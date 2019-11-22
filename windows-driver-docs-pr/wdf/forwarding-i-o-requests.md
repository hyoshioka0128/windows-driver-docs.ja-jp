---
title: I/O 要求の転送
description: I/O 要求の転送
ms.assetid: 75e007e3-1b97-44db-ac86-56aab78222a6
keywords:
- i/o 要求の転送 (WDK KMDF)
- I/o 要求 WDK KMDF、転送
- 要求の処理 WDK KMDF、転送 i/o 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ceca9fd5f7be2392c41c50f1cffd8be560e7f46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842853"
---
# <a name="forwarding-io-requests"></a>I/O 要求の転送





ドライバーは、処理できない i/o 要求を受信すると、通常、次のいずれかの操作を行います。

-   受信した要求を別のドライバーに転送します。

-   追加の要求を作成し、別のドライバーに送信します。

フレームワークベースのドライバーは、システム上の他のドライバーを表す[i/o ターゲットを使用し](using-i-o-targets.md)て要求を転送します。 ドライバーは、次の方法のいずれかを使用して、i/o ターゲットに要求を転送できます。

-   ドライバーは、 [**Wdfdevicegetiotarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)を呼び出し、その後に[**Wdfrequestformatrequestを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype)使用し、最後に[**wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出すことによって、i/o 要求を次の下位のドライバーに転送できます。

    この手法は、ドライバーが転送前に変更する必要がない要求を受信した場合にのみ役立ちます。

-   ドライバーは、 [**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)を呼び出してフィルタードライバーとして登録できます。

    フィルタードライバーが特定の種類の i/o 要求に対して i/o キューを提供しない場合、フレームワークはその種類の要求を次の下位のドライバーに自動的に転送します。

-   通常、関数ドライバーは、各 i/o 要求の内容を調べます。 関数ドライバーが要求を処理できない場合、要求が変更され、i/o ターゲットに転送される可能性があります。 または、1つまたは複数の新しい要求を作成し、それらを i/o ターゲットに送信する場合があります。

    フレームワークの i/o ターゲットオブジェクトは、他のドライバーに i/o 要求を送信するためのいくつかのメソッドを定義します。 たとえば、ドライバーは[**Wdfiotargetformatrequestforread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread)を呼び出した後、 [**wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して、読み取り要求を i/o ターゲットに送信することができます。 I/o ターゲットの詳細については、「 [I/o ターゲットの使用](using-i-o-targets.md)」を参照してください。

    多くの場合、ドライバーライターは、i/o ターゲットに要求を送信する前に、要求の基になる WDM [i/o スタック位置](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations)の内容を指定することが必要になることがあります。 このような場合は、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出す前に、ドライバーが[**Wdfrequestwdmformatを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmformatusingstacklocation)呼び出すことができます。

場合によっては、ドライバーが1つのコマンドをすべてのデバイスに送信する必要があるため、複数の i/o ターゲットに対して同じ要求を送信する必要があります。 I/o ターゲットに要求を送信する前に、ドライバーは[**Wdfrequestchangetarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestchangetarget)を呼び出して、i/o ターゲットにアクセスできることを確認できます。

ドライバーは、i/o ターゲットに転送するすべての要求を最終的に[完了](completing-i-o-requests.md)する必要があります。ただし、 [**WDF\_request\_send\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)を設定していない場合は、 [**wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出したときに\_と\_忘れるフラグ\_送信します。

ドライバーが要求を転送する場合、フレームワークは、送信元ドライバーから受信側ドライバーにフレームワーク要求オブジェクトを文字どおり転送しません。 代わりに、フレームワークは、要求を受信するドライバーに新しい要求オブジェクトを作成します。 要求の基になる i/o 要求パケット ([**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)) だけが、あるドライバーから別のドライバーに転送されます。

 

 






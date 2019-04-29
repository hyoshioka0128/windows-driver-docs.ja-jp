---
title: I/O 要求の転送
description: I/O 要求の転送
ms.assetid: 75e007e3-1b97-44db-ac86-56aab78222a6
keywords:
- WDK KMDF を要求する I/O の転送
- I/O 要求の転送の WDK KMDF
- WDK KMDF の処理、I/O 要求の転送要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a29f2a7cb3e2e3072bb642cf4be5e4492d126ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391352"
---
# <a name="forwarding-io-requests"></a>I/O 要求の転送





ドライバーでは、処理できない I/O 要求を受け取る、通常このファイルは、次のいずれか。

-   別のドライバーに受信した要求を転送します。

-   追加の要求を作成し、別のドライバーに送信します。

フレームワーク ベースのドライバーで要求を転送する[I/O ターゲットを使用して](using-i-o-targets.md)システム上の他のドライバーを表します。 ドライバーでは、次の手法を使用、I/O ターゲットへの要求を転送できます。

-   ドライバーは、呼び出すことによって、次の下位ドライバーへの I/O 要求を転送できます[ **WdfDeviceGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff546017)、その後に[ **WdfRequestFormatRequestUsingCurrentType**](https://msdn.microsoft.com/library/windows/hardware/ff549955)、最後に[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)します。

    この手法は、ドライバーが受信要求を転送する前に変更がない場合にのみ役立ちます。

-   ドライバーを呼び出すことができます[ **WdfFdoInitSetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff547273)フィルター ドライバーとして登録します。

    フィルター ドライバーが I/O 要求の特定の型の I/O キューを提供されていない場合、フレームワークは自動的に次の下位のドライバーには、その型の要求を転送します。

-   通常、関数のドライバーは、各 I/O 要求の内容を調べます。 関数のドライバーが要求を処理できない場合は、要求を修正し、I/O をターゲットに転送するがあります。 または、1 つまたは複数の新しい要求を作成し、I/O のターゲットに送信があります。

    フレームワークの I/O のターゲット オブジェクトは、他のドライバーに I/O 要求を送信するためのいくつかのメソッドを定義します。 たとえば、ドライバーを呼び出すことができます[ **WdfIoTargetFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff548612)、その後に[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)、読み取り要求を送信する、I/O のターゲット。 I/O のターゲットの詳細については、次を参照してください。[を使用して I/O ターゲット](using-i-o-targets.md)します。

    まれには、ドライバー開発者が、要求の基になる WDM の内容を指定する場合。 [I/O スタックの場所](https://msdn.microsoft.com/library/windows/hardware/ff551821)I/O のターゲットに要求を送信する前にします。 ドライバーを呼び出せるような場合、 [ **WdfRequestWdmFormatUsingStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550036)を呼び出す前に[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)します。

場合によっては、ドライバーをする必要があります同じ要求、I/O のいくつかのターゲットに通常ため、送信、ドライバーは、すべてのデバイスを 1 つのコマンドを送信する必要があります。 I/O のターゲットに要求を送信する前に、ドライバーを呼び出すことができます[ **WdfRequestChangeTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff549943) I/O ターゲットがアクセスできることを確認します。

ドライバーに最終的にする必要があります[完了](completing-i-o-requests.md)設定しない限り、I/O のターゲットに転送するすべての要求、 [ **WDF\_要求\_送信\_オプション\_送信\_AND\_破棄**](https://msdn.microsoft.com/library/windows/hardware/ff552493)フラグを呼び出すときに[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)します。

ドライバーは、要求を転送するときにフレームワークは文字どおりに転送されません framework 要求オブジェクト送信元のドライバーから受信側のドライバーに注意してください。 代わりに、フレームワークは、要求を受信したドライバーの新しい要求オブジェクトを作成します。 要求のみには、I/O 要求パケットの基になる ([**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)) が 1 つのドライバーから別に転送します。

 

 






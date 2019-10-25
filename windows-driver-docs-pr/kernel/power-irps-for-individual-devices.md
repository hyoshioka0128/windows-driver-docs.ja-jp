---
title: 個々のデバイスの電源 IRP
description: 個々のデバイスの電源 IRP
ms.assetid: a8d5db12-8f6b-4c65-9814-0bc3e476dd1c
keywords:
- パワー Irp WDK カーネル、デバイス
- デバイスの電源 Irp WDK カーネル
- 電源シーケンス値 WDK カーネル
- 動作状態は WDK 電源管理を返します
- 復帰デバイス
- ウェイクアップ機能 WDK の電源管理
- デバイスのウェイクアップと WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2064f6f032e0fca0c9a2008275f18e0076b4874
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838501"
---
# <a name="power-irps-for-individual-devices"></a>個々のデバイスの電源 IRP





*デバイスの電源 irp*では、主な irp コードの[**irp\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)、以下に一覧表示されているマイナー電源 irp コードの1つ、および**power. 型**メンバーの値**DevicePowerState**を指定します。

[**IRP\_\_クエリ\_電力**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

[**IRP\_\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

[**IRP\_\_待機\_ウェイク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)

[**IRP\_\_電源\_シーケンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)

デバイススタック内のすべてのドライバーは、このような Irp を受信します。通常、これらの Irp を送信できるのは、デバイスの電源ポリシーマネージャーだけです。 ただし、「[アイドル検出のための電源マネージャールーチンの使用](using-power-manager-routines-for-idle-detection.md)」で説明されているように、電源マネージャーはデバイスの代わりにアイドル検出を実行するときにデバイスの電源 IRP を送信できます。

ドライバーは、次のいずれかの理由でデバイスの電源 IRP を送信します。

-   システム電源 IRP に応答してデバイスの電源状態を照会または変更するには

-   電力を節約するためにデバイスをスリープ状態にするには

-   スリープ状態になった後にデバイスを動作状態に戻すには

-   外部信号に応答してデバイスを目覚めできるようにするには

-   デバイスの電源をオンにしたときに電源シーケンスの値を取得するには

次の図は、デバイスの電源 IRP を送信、転送、および完了するために実行される一連の手順を示しています。

![デバイスの電源のパスを示す図 (irp)](images/devpoirp.png)

前の図に示すように、デバイスの電源 IRP は、次の手順で送信、転送、および完了します。

1.  デバイスの電源ポリシー所有者は、 [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、irp のターゲットである PDO と、irp の完了時に呼び出されるコールバックルーチンを指定して、デバイスの電源 IRP を割り当てます。

2.  電源マネージャーによってデバイスの電源 (IRP) が割り当てられ、ターゲット PDO のデバイススタックの最上位のドライバーに送信されます。

3.  ドライバーは、次の操作を実行します。

    -   必要に応じて[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。

    -   完了ルーチンが使用されていない場合、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) (windows Server 2003、windows XP、および windows 2000) を呼び出します。 Windows Vista 以降では、この呼び出しは不要であり、このような呼び出しは電源管理操作を実行しません。

    -   は[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows 7 と windows Vista) を呼び出します。または、 [**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、IRP を次の下位のドライバーに渡します。

    スタック内の各ドライバーは、IRP がバスドライバーに到達するまで、これを行います。 ドライバーが IRP を失敗させる必要がある場合は、直ちに[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

4.  デバイス PDO を保持するバスドライバーは、要求されたアクションを実行し、 **IoCompleteRequest**を呼び出して IRP を完了します。 デバイスが取り外されているか、削除されている場合、バスドライバーはデバイスの電源投入の IRP を失敗させる可能性があります。

5.  I/o マネージャーは、IRP をスタックに渡したときにドライバーによって設定された*Iocompletion*ルーチンを呼び出します。 すべての*Iocompletion*ルーチンが呼び出されると、コールバックルーチンが実行されます。

デバイスの電源 Irp の詳細については、「[個々のデバイスの電源の管理](managing-power-for-individual-devices.md)」および「[ウェイクアップ機能を搭載したデバイスのサポート](supporting-devices-that-have-wake-up-capabilities.md)」を参照してください。 電源シーケンスの IRP の詳細については、「 [**irp\_\_電源\_シーケンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)」を参照してください。

 

 





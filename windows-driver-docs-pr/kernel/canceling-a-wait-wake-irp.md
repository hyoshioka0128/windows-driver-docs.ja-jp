---
title: 待機/ウェイク IRP のキャンセル
description: 待機/ウェイク IRP のキャンセル
ms.assetid: 08e1d11a-91a3-496a-b3ad-f99456e4ce1d
keywords:
- 電源管理 WDK カーネル、ウェイクアップ機能
- 外部ウェイクアップシグナル WDK
- 復帰デバイス
- ウェイクアップ機能 WDK の電源管理
- デバイスのウェイクアップと WDK の電源管理
- IRP_MN_WAIT_WAKE
- 待機/ウェイク Irp WDK 電源管理, 取り消し
- 待機/ウェイク Irp をキャンセルしています
- キャンセルルーチン、待機/ウェイク Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eabf931baf7b34d4a082c0477c6e8c4116341558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828550"
---
# <a name="canceling-a-waitwake-irp"></a>待機/ウェイク IRP のキャンセル





待機/ウェイク IRP を送信したドライバーだけが、その IRP をキャンセルできます。

ドライバーは、次のような状況で、保留中の待機/ウェイク IRP をキャンセルする必要がある場合があります。

-   ドライバーは、\_デバイス、irp\_[ **\_停止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)し、\_[**デバイスを削除\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)、 [**irp\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)を削除\_、PnP irp\_を受信します。、または IRP\_、デバイスの削除要求を[ **\_驚く\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)します。 ドライバーは、デバイスの再起動後に、待機/ウェイク IRP ([**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)) を再実行する必要があります。

-   システムはスリープ状態になりますが、システムのスリープ状態を解除するためにデバイスを有効にしないでください。

    たとえば、USB ハブのドライバーは、後で入力デバイスの1つをスリープ状態にする場合に備えて、デバイスの起動時に **\_ウェイク要求\_待機**するように、IRP\_を送信する可能性があります。 システムの状態が [稼働中] になっている間は、デバイスからのウェイク信号によってデバイスが動作中の状態に戻ります (ただし、システムの電源状態に影響はありません)。 システムをシャットダウンする準備ができたら、デバイスがシステムの停止を許可しない場合、USB ハブドライバーはこの IRP をキャンセルします。

-   システムはスリープ状態に入り、デバイスはデバイスを目覚めできません。 つまり、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造体で指定された[**systemwake**](systemwake.md)値よりも電力が低い状態になります。

-   デバイスは、ウェイクアップ信号に応答できない電源状態に入ります。 つまり、**デバイス\_機能**の構造で指定された[**devicewake**](devicewake.md)値よりも電力が低い状態になります。

待機/ウェイク IRP をキャンセルするには、IRP を送信したドライバーが[**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出し、以前に返された Irp に**PoRequestPowerIrp**という名前のポインターを渡します。

ドライバーは、送信されなかった wait/wake IRP をキャンセルすることはできません。

### <a href="" id="ddk-cancel-routines-for-wait-wake-irps-kg"></a>待機/ウェイク Irp のキャンセルルーチン

多くの関数およびバスドライバーでは、保留中の待機/ウェイク Irp に[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを設定する必要があります。次の種類のドライバーでは、このようなルーチンを設定する必要があります。

-   ウェイクアップを有効または無効にするためにデバイスの設定を変更するドライバー。

-   [**IRP\_完了\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)を送信するドライバーは、親デバイスのドライバーに対して\_ウェイク要求を待機します。

[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを使用すると、ドライバーはデバイスのウェイクアップを無効にし、保留中の待機/ウェイク IRP に関連するデータをクリーンアップすることができます。 親デバイスの待機/ウェイク Irp を要求するドライバーは、これらの Irp も取り消すことができます。

待機/ウェイク*キャンセル*ルーチンでは、ドライバーは次の手順を実行する必要があります。

1.  [**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出して、IRP の*キャンセル*ルーチンを**NULL**にリセットします。

2.  [**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出し、irp に指定されている**Cancelirql**を渡して、irp のキャンセルスピンロックを解放します。

3.  デバイス拡張機能の関連するフィールドをリセットします。 たとえば、待機/ウェイク IRP が保留中の場合、ほとんどのドライバーはフラグを設定し、デバイス拡張機能で IRP へのポインターを保持します。

    ドライバーが別の IRP をキャンセルしている間に、待機/ウェイク IRP を受信する可能性があることに注意してください。 ドライバーは、スピンロック保護 (またはそれと同等) の下に IRP が既に存在しているかどうかを確認する必要があります。 その場合は、ドライバーが適切な IRP をキャンセルするように、その処理を慎重に同期する必要があります。 *キャンセル*ルーチンでのスピンロックの使用の詳細については、「 [irp の取り消し](canceling-irps.md)」を参照してください。

4.  必要なデバイス設定を変更します。 たとえば、モデムドライバーはデバイスのウェイク設定を無効にします。

5.  **Irp&gt;iostatus に設定します。状態**は、\_取り消されました。

6.  [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、待機/ウェイク IRP を完了します。 IO\_\_増分は指定しません。

7.  ドライバーが以前に関連する Irp\_要求されている場合は、親デバイスに対して **\_ウェイク\_待機**します。ドライバーは、*キャンセル*ルーチン内からその irp をキャンセルする必要があります。 ドライバーは、親の IRP をキャンセルする前に、キャンセルスピンロックを解除する必要があります。

    たとえば、デバイスのバスドライバーとして機能し、その親の電源ポリシードライバーを所有するドライバーは、その親に送信された関連の待機/ウェイク IRP をキャンセルする必要があります。 [**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出すと、親の*キャンセル*ルーチンが呼び出され、デバイススタックが停止します。

 

 





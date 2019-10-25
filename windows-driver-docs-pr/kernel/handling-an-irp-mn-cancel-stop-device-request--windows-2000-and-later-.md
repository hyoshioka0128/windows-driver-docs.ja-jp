---
title: IRP_MN_CANCEL_STOP_DEVICE 要求の処理 (Windows 2000 以降)
description: IRP_MN_CANCEL_STOP_DEVICE 要求の処理 (Windows 2000 以降)
ms.assetid: 2e5e835f-d327-4bde-bdfd-8a71a47b0ac0
keywords:
- IRP_MN_CANCEL_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f805ca2b2cde39fd0fb20f557e73aced377eb5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838669"
---
# <a name="handling-an-irp_mn_cancel_stop_device-request-windows-2000-and-later"></a>IRP\_の処理\_キャンセル\_\_デバイス要求の停止 (Windows 2000 以降)





[**IRP\_\_キャンセル\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)の要求は、まずデバイスの親バスドライバーによって処理され、次にデバイススタック内の次の上位のドライバーごとに処理する必要があります。 ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで停止 irp を処理します。

IRP\_に応答して、 **\_デバイス要求の停止\_キャンセルする\_** 、ドライバーはデバイスを開始状態に戻して通常の操作を再開する必要があります。 ドライバーはキャンセル停止の IRP を正常に完了する必要があります。

ドライバーは、次のような手順を使用して、\_デバイスの要求を**中止\_\_をキャンセル、IRP\_** を処理します。

1.  低レベルのドライバーが再起動操作を完了するまで、デバイスの再起動を延期します。 ([低いドライバーが終了するまで、PNP IRP の処理を延期する](postponing-pnp-irp-processing-until-lower-drivers-finish.md)を参照してください。)

2.  ドライバーの実行が終了したら、デバイスを開始状態に戻します。

    正確な操作は、デバイスとドライバーによって異なります。

3.  IRP を保持するキューで Irp を開始します。

    デバイスが停止保留中の状態になっているときにドライバーが要求を保持していた場合は、[保留\_新しい\_要求] フラグをオフにし、IRP を保持するキューで Irp を開始します。 詳細について[は、「デバイスが一時停止したときの受信 irp の保持](holding-incoming-irps-when-a-device-is-paused.md)」を参照してください。

4.  [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用して IRP を完了します。

    -   関数またはフィルタードライバーの場合:

        ドライバーの[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)\_ルーチン[は、ドライバー](postponing-pnp-irp-processing-until-lower-drivers-finish.md)の*DispatchPnP*ルーチンがを呼び出す必要があるため、必要な\_処理\_より多くの処理を行います。**IoCompleteRequest**は、i/o 完了の処理を再開します。

        ドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。これにより、\_i/o の priority boost が\_インクリメントなしで**IoCompleteRequest**が呼び出され、その*DISPATCHPNP*ルーチンから status\_SUCCESS が返されます。

        ドライバーがこの操作を失敗させることはできません。 ドライバーが再起動 IRP に失敗すると、デバイスは不整合な状態になり、正常に動作しなくなります。

    -   親バスドライバーでは、次のようになります。

        ドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定し、IO\_\_priority boost を指定して**IoCompleteRequest**を呼び出します。 バスドライバーは、 *DispatchPnP*ルーチンから STATUS\_SUCCESS を返します。

        バスドライバーがこの操作を失敗させることはできません。 ドライバーが再起動 IRP に失敗すると、デバイスは不整合な状態になり、正常に動作しなくなります。

デバイスを起動してアクティブにすると、ドライバーが誤った取り消し停止要求を受け取ることがあります。 これは、たとえば、ドライバー (またはデバイススタックの上位にあるドライバー) が IRP\_に失敗した場合に発生する可能性があり[ **\_クエリ\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)の要求を停止します。 デバイスを起動してアクティブにすると、ドライバーは、デバイスの誤ったキャンセル/停止要求を安全に成功させることができます。

 

 





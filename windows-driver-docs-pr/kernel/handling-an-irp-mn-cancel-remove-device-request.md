---
title: IRP_MN_CANCEL_REMOVE_DEVICE 要求の処理
description: IRP_MN_CANCEL_REMOVE_DEVICE 要求の処理
ms.assetid: 3382c47d-6ac8-409e-b558-ad2f2ae83715
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE
- 誤ったキャンセル-削除要求の WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a9c06ef0d83e5b64ff26aa597e347f0f65c514
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836604"
---
# <a name="handling-an-irp_mn_cancel_remove_device-request"></a>IRP\_の処理\_キャンセル\_\_デバイス要求の削除





[**Irp\_が\_キャンセル\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)要求の削除に応答した場合、デバイスのドライバーは、irp\_を受信する前の状態にデバイスを返す必要があり\_**削除\_t_10_ DEVICE**要求。\_ 通常、ドライバーはデバイスを開始状態に戻します。

**\_キャンセル\_irp\_** 送信するだけでなく、デバイスに\_デバイスを削除すると、デバイスの削除関係に irp が送信されます (存在する場合)。 また、PnP マネージャーは、デバイスの子にキャンセル/削除の IRP を送信します。

PnP マネージャーは、 **IRP\_完了後\_キャンセル\_\_デバイス**要求の削除を完了した後に、任意の**Eventカテゴリ targetdevicechange**通知コールバックを呼び出します。 このようなコールバックは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出すことによってデバイスに登録されました。 また、PnP マネージャーは、 **RegisterDeviceNotification**を呼び出すことによって、このような通知に登録されているすべてのユーザーモードコンポーネントを呼び出します。

\_デバイスの要求を**削除\_削除する IRP\_\_** は、まずデバイスの親バスドライバーによって処理され、次にデバイススタック内の上位のドライバーによって処理される必要があります。 ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン内の irp の削除を処理します。

ドライバーは、 *DispatchPnP*ルーチンで次のような手順を使用して **\_デバイス要求を削除\_\_キャンセルする IRP\_** を処理します。

1.  関数またはフィルタードライバーで、下位のドライバーが再起動操作を完了するまで、デバイスの再起動を延期します。

    関数またはフィルタードライバーは、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、IRP\_完了した **\_キャンセル\_** デバイススタックからデバイスを\_削除します。すべての下位ドライバーが終了するまで、再起動操作を延期します。IRP. ([低いドライバーが終了するまで、PNP IRP の処理を延期する](postponing-pnp-irp-processing-until-lower-drivers-finish.md)を参照してください。)

2.  ドライバーの実行が終了したら、デバイスを以前の PnP 状態に戻します。

    ドライバーは、 **IRP\_\_** を受信する前の状態にデバイスを返し、\_デバイスの要求\_削除します。 通常、ドライバーはデバイスを開始状態に戻します。 正確な操作は、デバイスとドライバーによって異なります。

    デバイスで以前にウェイクアップが有効にされていた場合は、デバイスの電源ポリシー所有者 (通常は関数ドライバー) が IRP\_を送信して、ウェイクアップ[ **\_待機\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)ウェイクアップ要求を送信する必要があります。 詳細については、「[電源管理](implementing-power-management.md)」を参照してください。

3.  **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定し、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を使用して irp を完了します。

    すべての PnP IRP と同様に、バスドライバーは IRP を完了します。

    また、関数またはフィルタードライバーは IRP も完了します。これは、ドライバーの*Iocompletion*ルーチンが、必要な\_処理\_より多くのステータス\_を返すことによって完了処理を中断したためです。

    ドライバーは、この IRP を正常に完了する必要があります。 ドライバーがこの IRP に失敗した場合、デバイスは不整合な状態のままになります。

デバイスを起動してアクティブにすると、ドライバーが誤ったキャンセル/削除要求を受け取ることがあります。 これは、たとえば、ドライバー (またはデバイススタックの上位にあるドライバー) が IRP\_に失敗した場合に発生する可能性があり **\_クエリ\_\_デバイス**の要求を削除します。 デバイスを起動してアクティブにすると、ドライバーは、デバイスに対して誤ったキャンセル/削除要求を成功させるだけです。

 

 





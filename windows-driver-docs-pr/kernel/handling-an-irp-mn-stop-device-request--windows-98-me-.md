---
title: IRP_MN_STOP_DEVICE 要求の処理 (Windows 98/Me)
description: IRP_MN_STOP_DEVICE 要求の処理 (Windows 98/Me)
ms.assetid: 8e44561a-f494-48ce-ab61-aa47cd4e1c64
keywords:
- IRP_MN_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a41bb6a7cb878ba5c83c8dc2296e7ec4b9165ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369820"
---
# <a name="handling-an-irpmnstopdevice-request-windows-98me"></a>IRP の処理\_MN\_停止\_デバイス要求 (Windows 98/Me)





Windows 98 で PnP マネージャーは通常、送信、/、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)成功したクエリの停止後に要求します。 ただし、デバイス スタックが前回失敗した場合、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求、PnP マネージャーに送信する**IRP\_MN\_停止\_デバイス**前のクエリを使用せずに要求します。

**IRP\_MN\_停止\_デバイス**デバイス スタックの最上位のドライバーによって、各 [次へ] の下のドライバーでし、要求が最初に処理します。 ドライバーのハンドルに Irp の停止、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

ドライバーの処理、 **IRP\_MN\_停止\_デバイス**次のようなプロシージャを使って要求。

1.  デバイスが一時停止したことを確認します。

    かどうか、ドライバーが完全に一時停止しないへの応答でデバイスを[ **IRP\_MN\_クエリ\_停止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)要求、ここでは、する必要があります。

    デバイスが停止し、そのため、デバイスの状態を失う可能性がありますが、電源を失う可能性があります。 デバイスのドライバーが、デバイスの状態情報を保存する必要があり、後続の受信時に復元**IRP\_MN\_開始\_デバイス**要求。

2.  デバイスのハードウェア リソースを解放します。

    関数のドライバー、正確な操作は、デバイスとドライバーによって異なりますが、切断割り込みを含めることができます[ **IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)と物理アドレスの範囲を解放[ **MmUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)、I/O ポートを解放します。

    ドライバーがへの応答でリソースを解放する必要があります、フィルターまたはバス ドライバーに、デバイスのハードウェア リソースが取得される場合、 **IRP\_MN\_停止\_デバイス**要求。

3.  設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

4.  [次へ] の下のドライバーに IRP を渡すか、IRP を完了します。

    -   関数またはフィルター ドライバーでは、セットアップで [次へ] スタックの場所[ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で [次へ] の下位のドライバーに IRP を渡す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)からの状態を返すと**保留**から戻り値の状態として、 *DispatchPnP*ルーチン。 IRP を実行しないでください。

    -   バス ドライバーの完了を使用して、IRP [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IO と\_いいえ\_インクリメント演算子とからの戻り値、 *DispatchPnP*ルーチン。

ドライバーは、デバイスの停止中に、デバイスにアクセスする任意の Irp を開始できません。 ドライバーには、このような Irp が失敗する必要があります。

 

 





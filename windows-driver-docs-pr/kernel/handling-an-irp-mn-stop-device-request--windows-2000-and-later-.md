---
title: IRP_MN_STOP_DEVICE 要求の処理 (Windows 2000 以降)
description: IRP_MN_STOP_DEVICE 要求の処理 (Windows 2000 以降)
ms.assetid: 5e91748c-d03a-48f7-a9cc-df2801d8a555
keywords:
- IRP_MN_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e399fa2809870e8bb9c626dc4fff6f8c51021aca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355229"
---
# <a name="handling-an-irpmnstopdevice-request-windows-2000-and-later"></a>IRP の処理\_MN\_停止\_デバイス (Windows 2000 以降) を要求します。





[ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)デバイス スタックの最上位のドライバーによって、各 [次へ] の下のドライバーでし、要求が最初に処理します。 ドライバーのハンドルに Irp の停止、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

ドライバーの処理、 **IRP\_MN\_停止\_デバイス**次のようなプロシージャを使って要求。

1.  デバイスが一時停止したことを確認します。

    かどうか、ドライバーが完全に一時停止しないへの応答でデバイス、 [ **IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)要求、ここでは、する必要があります。 保持設定\_新規\_要求がデバイスの拡張機能のフラグし、デバイスを一時停止に必要なその他の操作を実行します。

    デバイスは、リソースに再調整操作中に電源を失う可能性があり、そのため、デバイスの状態を失う可能性があります。 デバイスのドライバーが、デバイスの状態情報を保存する必要があり、後続の受信時に復元[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。

2.  デバイスのハードウェア リソースを解放します。

    関数のドライバー、正確な操作は、デバイスとドライバーによって異なりますが、切断割り込みを含めることができます[ **IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)と物理アドレスの範囲を解放[ **MmUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)、I/O ポートを解放します。

    ドライバーがへの応答でリソースを解放する必要があります、フィルターまたはバス ドライバーに、デバイスのハードウェア リソースが取得される場合、 **IRP\_MN\_停止\_デバイス**要求。

3.  設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

4.  [次へ] の下のドライバーに IRP を渡すか、IRP を完了します。

    -   関数またはフィルター ドライバーでは、セットアップで [次へ] スタックの場所[ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で [次へ] の下位のドライバーに IRP を渡す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)からの状態を返すと**保留**から戻り値の状態として、 *DispatchPnP*ルーチン。 IRP を実行しないでください。

    -   バス ドライバーの完了を使用して、IRP [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IO と\_いいえ\_インクリメント演算子とからの戻り値、 *DispatchPnP*ルーチン。

リソースを再調整する、デバイスを停止すると、中に、ドライバーは、デバイスにアクセスする任意の Irp を開始できません。 」の説明に従って、ドライバーは、このような Irp をキューする必要があります[を保持している受信 Irp ときに、デバイスが一時停止](holding-incoming-irps-when-a-device-is-paused.md)、またはキュー、ドライバーは IRP を保持するを実装していない場合に、I/O 要求を削除する必要がありますしないと失敗します。

 

 





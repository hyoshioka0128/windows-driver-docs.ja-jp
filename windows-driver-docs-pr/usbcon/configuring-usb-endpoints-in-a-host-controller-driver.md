---
Description: UCX はエンドポイントオブジェクトの作成を管理し、ホストコントローラーに対して、プログラムのエンドポイントを USB ホストコントローラーにプログラムまたは破棄するように通知します。
title: USB ホスト コントローラー ドライバーでの USB エンドポイントの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4fda14fc82d162337d8f87f0e007fbb0ec91e35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842400"
---
# <a name="configure-usb-endpoints-in-a-usb-host-controller-driver"></a>USB ホスト コントローラー ドライバーでの USB エンドポイントの構成


UCX はエンドポイントオブジェクトの作成を管理し、ホストコントローラーに対して、プログラムのエンドポイントを USB ホストコントローラーにプログラムまたは破棄するように通知します。

エンドポイントがプログラミングされている間は、UCX によっても管理されます。 デバイスがバスに接続されて切断されると、エンドポイントの状態が変化し、中断やリセットなどの電源イベントが発生し、別の設定の変更など、新しいエンドポイントの作成が行われます。

## <a name="endpoint-configuration"></a>エンドポイントの構成


UCX は、ホストコントローラードライバーによって実装されたコールバック関数を呼び出し、エンドポイントが USB ホストコントローラーにプログラムする必要があるか、または解放されたことをドライバーに通知します。 [ *.Evt\_UCX\_USBDEVICE\_ENABLE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable)が呼び出されると、ドライバーはデバイスの既定のエンドポイントへの転送を実行するためのコントローラーを準備します。 コントローラーの準備には、既定のエンドポイントのプログラミングが含まれます。 [ *.Evt\_UCX\_USBDEVICE\_DISABLE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)が呼び出されると、ドライバーは既定のエンドポイントを破棄し、デバイスに関連付けられているその他のコントローラーリソースを解放します。 [ *.Evt\_UCX\_USBDEVICE\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure)が呼び出された場合、ドライバーには、コントローラーにプログラムを提供する既定以外のエンドポイントのリストが与えられ、既定以外のエンドポイントの一覧が表示されます。コントロール. ホストコントローラードライバーは、指定された既定以外のエンドポイントをコントローラーにプログラムし、既定以外のエンドポイント (他の一覧で指定) をコントローラーから削除します。

## <a name="queue-state-management"></a>キュー状態管理


UCX は、エンドポイントキューの状態の変更を実行するために、ホストコントローラードライバーによって実装されたコールバック関数を呼び出します。 次に、このドライバーは、UCX に与えられたエンドポイントキューと、ドライバー内で保持されている第2レベルのキューに対応するアクションを実行します。 エンドポイントキューは、次のシナリオで中止または削除されます。

-   USB デバイスクライアントドライバーは、\_\_パイプ要求を中止して、URB\_機能を送信します。
-   中断中。
-   デバイスが接続されているハブは、デバイスの切断を検出します。
-   選択インターフェイスの設定要求中。

キューの中止または消去についてホストコントローラードライバーに通知するには、UCX が[ *.evt\_ucx\_エンドポイント\_abort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort)または[ *.evt\_UCX\_エンドポイント\_消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)します。 後で、UCX によってエンドポイントキューが必要になった場合、UCX は[ *.evt\_ucx\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start)コールバックを呼び出して、キューを開始するようにドライバーに通知します。

## <a name="transfer-cancellation"></a>転送の取り消し


ホストコントローラードライバーによって GUID\_USB\_機能が宣言されているコントローラーの場合は\_\_TT\_\_非同期\_転送\_キャンセルでは、ドライバーは[**Ucxendpointの**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)必要な転送を呼び出し、 [ *.evt\_UCX\_エンドポイント\_OK\_を*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)実装して、非同期 (一括またはコントロール) USB をキャンセルするための\_転送をキャンセルする必要があります。トランザクショントランスレーター (TT) ハブの背後にある USB 完全または低速度のデバイスに転送します。 それ以外の場合、ドライバーは必要に応じて Ucxendpoint\_エンドポイントを取得するために**Ucxendpoint\_** を呼び出すことができます *\_OK\_をキャンセル\_取り消し*を示す通知\_転送します。このエンドポイントで転送が許可され、ドライバーは転送の取り消しを続行できます。 または、 **Ucxendpointの**必要になる転送を呼び出さずに、ドライバーが直接転送をキャンセルすることもできます。

ホストコントローラードライバーは、常にこの GUID の要求に失敗した場合、これらの2つの関数呼び出しを完全に無視できます。

ドライバーが[**Ucxendpointの必要な転送転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)を呼び出さない場合、ドライバーの[ *.evt\_UCX\_エンドポイント\_OK\_\_キャンセル\_転送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)コールバックは呼び出されず、コールバック時に NULL にすることができます。製品.

ドライバーが[**Ucxendpointの必要な転送転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)を使用する場合、ドライバーは、転送がコントローラーにプログラムされた後、キャンセルされたときに、 [ *.evt\_UCX\_エンドポイント\_OK を待機するときに、メソッドを呼び出す必要があり\_\_するには*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)、完了する前に\_転送をキャンセルします。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  




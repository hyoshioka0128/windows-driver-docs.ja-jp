---
Description: UCX では、エンドポイントのオブジェクトの作成を管理し、ホスト コント ローラーでの USB ホスト コント ローラーにエンドポイントを deprogram プログラムを通知します。
title: USB ホスト コントローラー ドライバーでの USB エンドポイントの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d001089c579a388c210380c1036cad4a018cf2d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384478"
---
# <a name="configure-usb-endpoints-in-a-usb-host-controller-driver"></a>USB ホスト コントローラー ドライバーでの USB エンドポイントの構成


UCX では、エンドポイントのオブジェクトの作成を管理し、ホスト コント ローラーでの USB ホスト コント ローラーにエンドポイントを deprogram プログラムを通知します。

これによっては、エンドポイントのプログラムを作成中に、UCX によって管理されます。 エンドポイントの変更の状態のデバイスに接続するいるし、バスから切断電源イベントなど、中断をリセットして新しいエンドポイントの作成などの代替設定の変更が行われますが発生します。

## <a name="endpoint-configuration"></a>エンドポイントの構成


UCX では、ドライバーのエンドポイントにする必要がありますが、USB ホスト コント ローラーにプログラムまたはリリースに通知するホスト コント ローラー ドライバーによって実装されるコールバック関数を呼び出します。 ときに[ *EVT\_UCX\_USBDEVICE\_を有効にする*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable)が呼び出されると、ドライバー、コント ローラーの準備、デバイスの既定のエンドポイントへの転送を実行します。 コント ローラーを準備するには、既定のエンドポイントのプログラミングが含まれます。 ときに[ *EVT\_UCX\_USBDEVICE\_を無効にする*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)が呼び出されると、ドライバーは、既定のエンドポイントを deprograms しに関連付けられているその他のコント ローラーのリソースを解放しますデバイスです。 ときに[ *EVT\_UCX\_USBDEVICE\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure)が呼び出されると、ドライバーにプログラムを既定以外のエンドポイントの一覧を指定は、コント ローラー、コント ローラーから削除する既定以外のエンドポイントの別のリストを指定します。 ホスト コント ローラーのドライバーは、コント ローラーに、指定した既定以外のエンドポイントをプログラムし、(その他のリストで指定された) 既定以外のエンドポイントをコント ローラーからも削除されます。

## <a name="queue-state-management"></a>キューの状態の管理


UCX では、エンドポイントのキューの状態への変更を実行するホスト コント ローラー ドライバーによって実装されるコールバック関数を呼び出します。 ドライバーでは、ドライバー内で保持第 2 レベルのキューと UCX に指定されたエンドポイントのキューに対応する操作を行います。 エンドポイントのキューは中止または、これらのシナリオで消去します。

-   USB デバイスのクライアント ドライバーの送信、URB\_関数\_中止\_パイプ要求。
-   で中断します。
-   デバイスを接続するのには、ハブがデバイスの切断を検出した場合。
-   選択インターフェイス設定の要求中にです。

UCX を呼び出して、キューの中止または消去について、ホスト コント ローラーのドライバーを通知する[ *EVT\_UCX\_エンドポイント\_中止*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort)または[ *EVT\_UCX\_エンドポイント\_パージ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)します。 ある UCX でエンドポイント キューが必要な時点で後で、UCX が呼び出される場合、 [ *EVT\_UCX\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start)ドライバーに通知するコールバック、キューです。

## <a name="transfer-cancellation"></a>転送のキャンセル


ホスト コント ローラーのドライバーが GUID を宣言する任意のコント ローラーの\_USB\_機能\_クリア\_TT\_バッファー\_ON\_ASYNC\_転送\_CANCEL、ドライバーが呼び出す必要があります[ **UcxEndpointNeedToCancelTransfers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)実装と[ *EVT\_UCX\_エンドポイント\_OK\_TO\_キャンセル\_転送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers) usb の完全な非同期 (一括またはコントロール) USB 転送または低速デバイスの背後にあるをキャンセルする、トランザクションのトランスレーター (TT) ハブです。 その他のすべてのケースで、ドライバーは呼び出すことが必要に応じて**UcxEndpointNeedToCancelTransfers**を取得する、 *EVT\_UCX\_エンドポイント\_OK\_TO\_キャンセル\_転送*通知を転送をキャンセルはこのエンドポイントで許可されて、ドライバーは、転送がキャンセルに進むことがあることを示します。 または、ドライバーは呼び出さずに直接転送をキャンセルできます**UcxEndpointNeedToCancelTransfers**します。

ホスト コント ローラーのドライバーには、常にこの GUID の要求が失敗した場合、これらの 2 つの関数呼び出しを完全に無視できます。

場合は、ドライバーが呼び出すことはありません[ **UcxEndpointNeedToCancelTransfers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)、ドライバーの[ *EVT\_UCX\_エンドポイント\_[ok]\_\_キャンセル\_転送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)コールバックが呼び出されないと、コールバックの登録中に NULL を指定できます。

ドライバーが使用する場合[ **UcxEndpointNeedToCancelTransfers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)ドライバーは、転送をコント ローラーにプログラムを作成し、キャンセルし、メソッドを待機を呼び出す必要があります[ *EVT\_UCX\_エンドポイント\_OK\_TO\_キャンセル\_転送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)が完了する前にします。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  




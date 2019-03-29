---
Description: UCX manages the creation of endpoint objects, and notifies the host controller to program or deprogram endpoints into the USB host controller.
title: USB ホスト コントローラー ドライバーでの USB エンドポイントの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29d469172f86af57ac941a33bdb8f94da19e0c4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578086"
---
# <a name="configure-usb-endpoints-in-a-usb-host-controller-driver"></a>USB ホスト コントローラー ドライバーでの USB エンドポイントの構成


UCX では、エンドポイントのオブジェクトの作成を管理し、ホスト コント ローラーでの USB ホスト コント ローラーにエンドポイントを deprogram プログラムを通知します。

これによっては、エンドポイントのプログラムを作成中に、UCX によって管理されます。 エンドポイントの変更の状態のデバイスに接続するいるし、バスから切断電源イベントなど、中断をリセットして新しいエンドポイントの作成などの代替設定の変更が行われますが発生します。

## <a name="endpoint-configuration"></a>エンドポイントの構成


UCX では、ドライバーのエンドポイントにする必要がありますが、USB ホスト コント ローラーにプログラムまたはリリースに通知するホスト コント ローラー ドライバーによって実装されるコールバック関数を呼び出します。 ときに[ *EVT\_UCX\_USBDEVICE\_を有効にする*](https://msdn.microsoft.com/library/windows/hardware/mt187841)が呼び出されると、ドライバー、コント ローラーの準備、デバイスの既定のエンドポイントへの転送を実行します。 コント ローラーを準備するには、既定のエンドポイントのプログラミングが含まれます。 ときに[ *EVT\_UCX\_USBDEVICE\_を無効にする*](https://msdn.microsoft.com/library/windows/hardware/mt187840)が呼び出されると、ドライバーは、既定のエンドポイントを deprograms しに関連付けられているその他のコント ローラーのリソースを解放しますデバイスです。 ときに[ *EVT\_UCX\_USBDEVICE\_エンドポイント\_構成*](https://msdn.microsoft.com/library/windows/hardware/mt187842)が呼び出されると、ドライバーにプログラムを既定以外のエンドポイントの一覧を指定は、コント ローラー、コント ローラーから削除する既定以外のエンドポイントの別のリストを指定します。 ホスト コント ローラーのドライバーは、コント ローラーに、指定した既定以外のエンドポイントをプログラムし、(その他のリストで指定された) 既定以外のエンドポイントをコント ローラーからも削除されます。

## <a name="queue-state-management"></a>キューの状態の管理


UCX では、エンドポイントのキューの状態への変更を実行するホスト コント ローラー ドライバーによって実装されるコールバック関数を呼び出します。 ドライバーでは、ドライバー内で保持第 2 レベルのキューと UCX に指定されたエンドポイントのキューに対応する操作を行います。 エンドポイントのキューは中止または、これらのシナリオで消去します。

-   USB デバイスのクライアント ドライバーの送信、URB\_関数\_中止\_パイプ要求。
-   で中断します。
-   デバイスを接続するのには、ハブがデバイスの切断を検出した場合。
-   選択インターフェイス設定の要求中にです。

UCX を呼び出して、キューの中止または消去について、ホスト コント ローラーのドライバーを通知する[ *EVT\_UCX\_エンドポイント\_中止*](https://msdn.microsoft.com/library/windows/hardware/mt187825)または[ *EVT\_UCX\_エンドポイント\_パージ*](https://msdn.microsoft.com/library/windows/hardware/mt187827)します。 ある UCX でエンドポイント キューが必要な時点で後で、UCX が呼び出される場合、 [ *EVT\_UCX\_エンドポイント\_開始*](https://msdn.microsoft.com/library/windows/hardware/mt187829)ドライバーに通知するコールバック、キューです。

## <a name="transfer-cancellation"></a>転送のキャンセル


ホスト コント ローラーのドライバーが GUID を宣言する任意のコント ローラーの\_USB\_機能\_クリア\_TT\_バッファー\_ON\_ASYNC\_転送\_CANCEL、ドライバーが呼び出す必要があります[ **UcxEndpointNeedToCancelTransfers** ](https://msdn.microsoft.com/library/windows/hardware/mt188042)実装と[ *EVT\_UCX\_エンドポイント\_OK\_TO\_キャンセル\_転送*](https://msdn.microsoft.com/library/windows/hardware/mt187826) usb の完全な非同期 (一括またはコントロール) USB 転送または低速デバイスの背後にあるをキャンセルする、トランザクションのトランスレーター (TT) ハブです。 その他のすべてのケースで、ドライバーは呼び出すことが必要に応じて**UcxEndpointNeedToCancelTransfers**を取得する、 *EVT\_UCX\_エンドポイント\_OK\_TO\_キャンセル\_転送*通知を転送をキャンセルはこのエンドポイントで許可されて、ドライバーは、転送がキャンセルに進むことがあることを示します。 または、ドライバーは呼び出さずに直接転送をキャンセルできます**UcxEndpointNeedToCancelTransfers**します。

ホスト コント ローラーのドライバーには、常にこの GUID の要求が失敗した場合、これらの 2 つの関数呼び出しを完全に無視できます。

場合は、ドライバーが呼び出すことはありません[ **UcxEndpointNeedToCancelTransfers**](https://msdn.microsoft.com/library/windows/hardware/mt188042)、ドライバーの[ *EVT\_UCX\_エンドポイント\_[ok]\_\_キャンセル\_転送*](https://msdn.microsoft.com/library/windows/hardware/mt187826)コールバックが呼び出されないと、コールバックの登録中に NULL を指定できます。

ドライバーが使用する場合[ **UcxEndpointNeedToCancelTransfers**](https://msdn.microsoft.com/library/windows/hardware/mt188042)ドライバーは、転送をコント ローラーにプログラムを作成し、キャンセルし、メソッドを待機を呼び出す必要があります[ *EVT\_UCX\_エンドポイント\_OK\_TO\_キャンセル\_転送*](https://msdn.microsoft.com/library/windows/hardware/mt187826)が完了する前にします。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  




---
Description: UCX はルートハブの管理を実行します。
title: USB ホスト コントローラー ドライバー用のルート ハブ コールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a09d20835a15d77e7b8768d2d598007456acd56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837659"
---
# <a name="root-hub-callback-functions-of-a-usb-host-controller-driver"></a>USB ホスト コントローラー ドライバー用のルート ハブ コールバック関数


UCX はルートハブの管理を実行します。 仮想コントロールと割り込みエンドポイントをシミュレートし、管理します。 UCX は、ホストコントローラードライバーがルートハブオブジェクトを作成するときに、これらの仮想エンドポイントを作成します。

USB ハブドライバーは、通常のハブデバイスと通信するのと同じ方法でルートハブと通信します。 ただし、ホストコントローラードライバーは、ルートハブに送信された要求を制御および割り込みエンドポイントに直接処理する必要はありません。 UCX は、これらの要求を処理します。 UCX は、ホストコントローラーのポートの現在の状態に関する関連情報を返すことができるように、ホストコントローラードライバーによって実装されるコールバック関数を呼び出します。 これらのコールバック関数が完了すると、基になる UCX 要求が完了し、ハブドライバーに返されます。

ルートハブの割り込み転送を受信すると、UCX は要求を保留中として設定します。 ルートハブポートのいずれかで変更が検出されると、ホストコントローラードライバーは[**UcxRootHubPortChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nf-ucxroothub-ucxroothubportchanged)を呼び出します。 次に UCX は、ドライブの[ *.evt\_ucx\_ROOTHUB\_INTERRUPT\_TX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx)コールバックを呼び出します。ドライバーは、変更されたポートを示します。 この時点で、UCX は、保留中の要求をハブドライバーに返します。 ハブドライバーは、変更を通知したポートのポートの状態を取得するために、ルートハブに制御転送を送信します。 転送要求を保留中に制御し、ドライバーの[ *.evt\_ucx\_ROOTHUB\_コントロール\_URB*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb)コールバック関数を呼び出す ucx セット。 の実装では、デバイスが接続されていることを示すなど、ルートハブポートの現在の状態が返されます。 UCX は、ハブドライバーへの制御転送要求を完了し、デバイスの列挙を続行します。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  




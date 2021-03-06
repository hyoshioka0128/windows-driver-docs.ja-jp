---
Description: UCX は、ルート ハブの管理を実行します。
title: USB ホスト コントローラー ドライバー用のルート ハブ コールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66c499f43cd6e7dc45541943d11bf8d89867969d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364820"
---
# <a name="root-hub-callback-functions-of-a-usb-host-controller-driver"></a>USB ホスト コントローラー ドライバー用のルート ハブ コールバック関数


UCX は、ルート ハブの管理を実行します。 シミュレートし、コントロールや割り込みの仮想エンドポイントを管理します。 UCX は、ホスト コント ローラーのドライバーは、ハブのルート オブジェクトを作成するときに、それらの仮想エンドポイントを作成します。

USB ハブのドライバーは、通常のハブのデバイスと対話するのと同じ方法でルート ハブと対話します。 ただし、ホスト コント ローラーのドライバー コントロールおよび割り込みのエンドポイントのルート ハブに直接送信要求を処理する必要はありません。 UCX では、それらの要求を処理します。 UCX では、ホスト コント ローラーのポートの現在の状態に関連する情報を返せるようにホスト コント ローラーのドライバーによって実装されるコールバック関数を呼び出します。 これらのコールバック関数が完了したら、基になる UCX 要求が完了し、ハブのドライバーに返されます。

ルート ハブ、割り込みの転送を受信するには、UCX は保留中として要求を設定します。 1 つのルート ハブのポートの変更が検出されると、ホスト コント ローラーのドライバーを呼び出す[ **UcxRootHubPortChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nf-ucxroothub-ucxroothubportchanged)します。 UCX が呼び出され、ドライバーの[ *EVT\_UCX\_ROOTHUB\_INTERRUPT\_TX* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx)コールバック、およびドライバーを示しますが、変更されたポート. この時点では、UCX はハブのドライバーに保留中の要求を完了します。 ハブのドライバーでは、変更を通知するポートのポートの状態を取得する、ルート ハブにコントロール転送を送信します。 UCX がそのコントロールの転送要求を保留中に設定し、呼び出すドライバーの[ *EVT\_UCX\_ROOTHUB\_コントロール\_URB* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb)コールバック関数。 実装では、ハブのポート、デバイスが接続されていることを示す値を含む、ルートの現在の状態を返します。 UCX がハブのドライバーにコントロールの転送要求を完了し、デバイスの列挙が続行されます。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  




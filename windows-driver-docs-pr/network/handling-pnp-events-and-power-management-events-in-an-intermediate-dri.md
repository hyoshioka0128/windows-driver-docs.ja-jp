---
title: 中間ドライバーでの PnP イベントおよび電源管理イベントの処理
description: 中間ドライバーでの PnP イベントおよび電源管理イベントの処理
ms.assetid: 0b4cf76f-a31d-4cf6-8486-090393404af9
keywords:
- 中間ドライバー WDK ネットワー キング、イベント
- NDIS 中間ドライバー WDK、イベント
- プラグ アンド プレイ WDK、中間ネットワーク ドライバー
- 電源管理の WDK、中間ネットワーク ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6db058d5a2df5d18ce3ea181ad7d58f8c8d82fd3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379773"
---
# <a name="handling-pnp-events-and-power-management-events-in-an-intermediate-driver"></a>中間ドライバーでの PnP イベントおよび電源管理イベントの処理





中間のドライバーは、プラグ アンド プレイ (PnP) イベントおよび電源管理イベントを処理できる必要があります。 具体的には、次のとおりです。

-   中間のドライバーは、NDIS を設定する必要があります\_ミニポート\_属性\_いいえ\_HALT\_ON\_で SUSPEND フラグ、 **AttributeFlags**のメンバー、[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)に渡される構造[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。 詳細については、次を参照してください。[ミニポートとして初期化](initializing-virtual-miniports.md)します。

-   中間のドライバーの仮想ミニポート OID を処理する必要があります\_PNP\_*Xxx*要求。

-   中間のドライバーのプロトコルのセクションは、適切な OID を伝達する\_PNP\_*Xxx*を基になるミニポート ドライバーに要求します。 中間のドライバーの仮想ミニポートは、要求を開始したプロトコル ドライバーに基になるミニポート ドライバーの応答は、これらの要求を渡す必要があります。 中間のドライバーをデザインして不要な要求を渡す必要はありません。 たとえば、アプリケーションの負荷分散のフェールオーバー (LBFO) のように仮想ミニポートと基になるミニポート アダプター間の一対一のリレーションシップがない場合です。

-   中間のドライバーのプロトコルの一部を指定する必要があります、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)関数。

特定の順序では、中間ドライバーのプロトコルおよびミニポートのイベント ハンドラーは呼び出されません。 それに応じて中間ドライバー用のイベント ハンドラーを実装する必要があります。

ここでは、次のトピックについて説明します。

[電源管理イベントおよび処理 PnP に中間のドライバーの初期化](initializing-intermediate-drivers-to-handle-pnp-and-power-management-events.md)

[OID の処理\_PNP\_Xxx クエリとセット](handling-oid-pnp-xxx-queries-and-sets.md)

[中間のドライバーで ProtocolNetPnPEvent ハンドラーを実装します。](implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver.md)

[セットの電力要求を処理](handling-a-set-power-request.md)

 

 






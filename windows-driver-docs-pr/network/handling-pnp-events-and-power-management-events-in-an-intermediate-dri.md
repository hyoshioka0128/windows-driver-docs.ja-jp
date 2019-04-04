---
title: PnP イベントおよび中間のドライバーで電源管理イベントの処理
description: PnP イベントおよび中間のドライバーで電源管理イベントの処理
ms.assetid: 0b4cf76f-a31d-4cf6-8486-090393404af9
keywords:
- 中間ドライバー WDK ネットワー キング、イベント
- NDIS 中間ドライバー WDK、イベント
- プラグ アンド プレイ WDK、中間ネットワーク ドライバー
- 電源管理の WDK、中間ネットワーク ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3818224c408160c34a8f3b2af0999276ebb4ffa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557740"
---
# <a name="handling-pnp-events-and-power-management-events-in-an-intermediate-driver"></a>PnP イベントおよび中間のドライバーで電源管理イベントの処理





中間のドライバーは、プラグ アンド プレイ (PnP) イベントおよび電源管理イベントを処理できる必要があります。 具体的には、次のとおりです。

-   中間のドライバーは、NDIS を設定する必要があります\_ミニポート\_属性\_いいえ\_HALT\_ON\_で SUSPEND フラグ、 **AttributeFlags**のメンバー、[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)に渡される構造[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)します。 詳細については、[ミニポートとして初期化](initializing-virtual-miniports.md)を参照してください。

-   中間のドライバーの仮想ミニポート OID を処理する必要があります\_PNP\_*Xxx*要求。

-   中間のドライバーのプロトコルのセクションは、適切な OID を伝達する\_PNP\_*Xxx*を基になるミニポート ドライバーに要求します。 中間のドライバーの仮想ミニポートは、要求を開始したプロトコル ドライバーに基になるミニポート ドライバーの応答は、これらの要求を渡す必要があります。 中間のドライバーをデザインして不要な要求を渡す必要はありません。 たとえば、アプリケーションの負荷分散のフェールオーバー (LBFO) のように仮想ミニポートと基になるミニポート アダプター間の一対一のリレーションシップがない場合です。

-   中間のドライバーのプロトコルの一部を指定する必要があります、 [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)関数。

特定の順序では、中間ドライバーのプロトコルおよびミニポートのイベント ハンドラーは呼び出されません。 それに応じて中間ドライバー用のイベント ハンドラーを実装する必要があります。

ここでは、次のトピックについて説明します。

[電源管理イベントおよび処理 PnP に中間のドライバーの初期化](initializing-intermediate-drivers-to-handle-pnp-and-power-management-events.md)

[OID の処理\_PNP\_Xxx クエリとセット](handling-oid-pnp-xxx-queries-and-sets.md)

[中間のドライバーで ProtocolNetPnPEvent ハンドラーを実装します。](implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver.md)

[セットの電力要求を処理](handling-a-set-power-request.md)

 

 






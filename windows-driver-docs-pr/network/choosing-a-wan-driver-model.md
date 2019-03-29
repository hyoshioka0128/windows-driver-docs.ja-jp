---
title: WAN ドライバー モデルの選択
description: WAN ドライバー モデルの選択
ms.assetid: 63976cfa-6f7b-44d0-a4c5-de82254bedbd
keywords:
- WAN ミニポート ドライバー WDK ネットワー キング、ドライバー モデル
- WAN ミニポート ドライバー WDK ネットワー キング、NDIS WAN vs いる CoNDIS WAN ドライバー
- ドライバーは、WDK WAN をモデル化します。
- いる CoNDIS ドライバー WDK のネットワーク、WAN のドライバー
- いる CoNDIS WAN ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee4578db0bbfc142fde6664de4afb52238e4d6da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571959"
---
# <a name="choosing-a-wan-driver-model"></a>WAN ドライバー モデルの選択





Microsoft Windows 2000 と以降のオペレーティング システムは、2 つの WAN ドライバー モデルをサポートします。NDIS WAN といる CoNDIS WAN します。

NDIS WAN ミニポート ドライバーは、コネクションレス ミニポート ドライバーの NDIS モデルに基づいて構築されます。 NDIS WAN ミニポート ドライバーでは、NDIS version 5.0 とそれ以降のドライバーのサポートされていません。 新しいドライバーは、いる CoNDIS WAN のドライバーのアーキテクチャに基づいている必要があります。

いる CoNDIS WAN ドライバーは、接続指向 (いる CoNDIS) NDIS ドライバー モデルに基づいて構築されます。

いる CoNDIS WAN ミニポート ドライバーおよびミニポート コール マネージャー (MCMs) を実行できます。

-   接続指向の非 WAN ミニポート ドライバーを呼び出すのと同じ NDIS 関数を呼び出します。

-   同じセットをエクスポート*MiniportXxx* wan を経由の接続指向のミニポート ドライバーをエクスポートする関数。

-   WAN に固有の追加機能を提供します。

いる CoNDIS ドライバーの詳細については、次を参照してください。 [Connection-Oriented NDIS](connection-oriented-ndis.md)します。

新しい WAN ドライバーを作成する場合は、WAN いる CoNDIS モデルを使用することをお勧めします。

Microsoft では、引き続き既存の NDIS WAN ミニポート ドライバーのサポートします。 古いハードウェアのいる CoNDIS ドライバーを記述する必要はありません。

次のトピックでは、WAN いる CoNDIS モデルを使用しての主な利点について説明します。

[いる CoNDIS WAN がより柔軟です](condis-wan-is-more-flexible.md)

[WAN いる CoNDIS ほど複雑では](condis-wan-is-less-complex.md)

[いる CoNDIS WAN の他の特典](other-benefits-of-condis-wan.md)

[いる CoNDIS WAN ドライバーが利用できるその他の NDIS 機能](other-ndis-features-available-to-condis-wan-drivers.md)

 

 






---
title: WAN ドライバーモデルの選択の概要
description: WAN ドライバーモデルの選択の概要
ms.assetid: 63976cfa-6f7b-44d0-a4c5-de82254bedbd
keywords:
- WAN ミニポートドライバー WDK ネットワーク、ドライバーモデル
- WAN ミニポートドライバー WDK ネットワーク、NDIS WAN、および WAN ドライバー
- ドライバーモデルの WDK WAN
- CoNDIS ドライバー WDK ネットワーク、WAN ドライバー
- CoNDIS WAN ドライバーの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78cbcba80d7da682faa446fdba7b10bb88dc3d9e
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565687"
---
# <a name="introduction-to-choosing-a-wan-driver-model"></a>WAN ドライバーモデルの選択の概要





Microsoft Windows 2000 以降のオペレーティングシステムでは、次の2つの WAN ドライバーモデルがサポートされています。NDIS WAN と CoNDIS WAN です。

NDIS WAN ミニポートドライバーは、コネクションレスミニポートドライバーの NDIS モデルに基づいて構築されています。 Ndis WAN ミニポートドライバーは、NDIS バージョン5.0 以降のドライバーではサポートされていません。 新しいドライバーは、CoNDIS WAN ドライバーのアーキテクチャに基づいている必要があります。

CoNDIS WAN ドライバーは、接続指向の NDIS (condis ドライバーモデルに基づいて構築されています。

CoNDIS WAN ミニポートドライバーとミニポートコールマネージャー (MCMs) は次のことができます。

-   非 WAN 接続指向ミニポートドライバーが呼び出すのと同じ NDIS 関数を呼び出します。

-   WAN 以外の接続指向のミニポートドライバーでエクスポートされたのと同じ*Miniportxxx*関数のセットをエクスポートします。

-   WAN 固有の追加機能を提供します。

CoNDIS ドライバーの詳細については、「[接続指向 NDIS](connection-oriented-ndis.md)」を参照してください。

新しい WAN ドライバーを作成する場合は、Conconwan モデルを使用することをお勧めします。

Microsoft は、引き続き既存の NDIS WAN ミニポートドライバーをサポートします。 古いハードウェア用に CoNDIS ドライバーを作成する必要はありません。

次のトピックでは、CoNDIS WAN モデルを使用する主な利点について説明します。

[CoNDIS WAN の柔軟性が向上](condis-wan-is-more-flexible.md)

[CoNDIS WAN の複雑さが低い](condis-wan-is-less-complex.md)

[CoNDIS WAN のその他のメリット](other-benefits-of-condis-wan.md)

[WAN ドライバーで使用できるその他の NDIS 機能](other-ndis-features-available-to-condis-wan-drivers.md)

 

 






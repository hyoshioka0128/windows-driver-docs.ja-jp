---
title: NDIS 中間ドライバーガイド
description: NDIS 中間ドライバーガイド
ms.assetid: 773d9711-fdea-4541-bb0d-6b07b50892fc
keywords:
- 中間ドライバー WDK ネットワーク
- ネットワークドライバー WDK、中間ドライバー
- NDIS WDK、中間ドライバー
- NDIS 中間ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba6624c9fde2757958ffe46e2ac543fc9f15941f
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565652"
---
# <a name="ndis-intermediate-drivers-guide"></a>NDIS 中間ドライバーガイド

上層プロトコルドライバーとミニポートドライバーの間の NDIS 中間ドライバーインターフェイス。 中間ドライバーを必要とするアプリケーションには、次のようなものがあります。

-   古いトランスポートドライバーと、トランスポートドライバーに不明なメディアの種類を管理するミニポートドライバーとの間のメディア変換。

-   セキュリティまたはその他の目的のためのデータフィルタリング。

-   負荷分散フェールオーバー (LBFO) ソリューション。

-   ネットワークデータの統計情報の監視と収集。

中間ドライバーの記述を試行する前に、「NDIS ミニポートとプロトコルドライバーについて」を参照してください。 NDIS ミニポートドライバーの詳細については、「 [Ndis ミニポートドライバー](ndis-miniport-drivers.md)」を参照してください。 NDIS プロトコルドライバーの詳細については、「 [Ndis プロトコルドライバー](ndis-protocol-drivers.md)」を参照してください。

次のセクションでは、中間ドライバーを紹介し、そのようなドライバーを作成およびインストールする方法について説明します。

[NDIS 中間ドライバーを開発するためのロードマップ](roadmap-for-developing-ndis-intermediate-drivers.md)

[NDIS 中間ドライバーの概要](introduction-to-ndis-intermediate-drivers.md)

[NDIS 中間ドライバーの記述](writing-ndis-intermediate-drivers.md)

[中間ドライバー設計の概念](intermediate-driver-design-concepts.md)

[中間ドライバーのインストール](installing-an-intermediate-driver.md)

 

 






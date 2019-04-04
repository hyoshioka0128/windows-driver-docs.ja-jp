---
title: NDIS 中間ドライバ
description: NDIS 中間ドライバ
ms.assetid: 773d9711-fdea-4541-bb0d-6b07b50892fc
keywords:
- 中間ドライバー WDK ネットワーク
- ネットワーク ドライバー WDK、中間ドライバー
- WDK NDIS 中間ドライバ
- NDIS 中間ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4393badc6ca918eaf0ecf5120de93f329f5d587b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528973"
---
# <a name="ndis-intermediate-drivers"></a>NDIS 中間ドライバ





上位レベルのプロトコルおよびミニポートのドライバーの間で NDIS 中間ドライバ インターフェイスです。 中間のドライバーを必要とする一部のアプリケーションは次のとおりです。

-   古いトランスポート ドライバーとトランスポート ドライバーに不明なメディアの種類を管理するミニポート ドライバー間の変換をメディア。

-   データのセキュリティまたはその他の目的でフィルター処理します。

-   分散フェールオーバー (LBFO) のソリューションを読み込みます。

-   の監視とネットワーク データの統計の収集

中間のドライバーを作成する前に、NDIS ミニポートとプロトコル ドライバーについてお読みください。 NDIS ミニポート ドライバーの詳細については、[NDIS ミニポート ドライバー](ndis-miniport-drivers.md)を参照してください。 NDIS プロトコル ドライバーの詳細については、[NDIS プロトコル ドライバー](ndis-protocol-drivers.md)を参照してください。

次のセクションでは、中間ドライバーを紹介し、作成し、このようなドライバーをインストールする方法について説明します。

[NDIS 中間ドライバを開発するためのロードマップ](roadmap-for-developing-ndis-intermediate-drivers.md)

[NDIS 中間ドライバの概要](introduction-to-ndis-intermediate-drivers.md)

[書き込み NDIS 中間ドライバ](writing-ndis-intermediate-drivers.md)

[中間ドライバー設計の概念](intermediate-driver-design-concepts.md)

[中間のドライバーをインストールします。](installing-an-intermediate-driver.md)

 

 






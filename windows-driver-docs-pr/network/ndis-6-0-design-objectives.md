---
title: NDIS 6.0 の設計目標
description: NDIS 6.0 の設計目標
ms.assetid: 1b59bc97-be79-47ba-8e39-208a9d38f6b9
keywords:
- NDIS WDK、NDIS について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dccf5382b1a2308ac2843dcb626e41275dc5fb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383615"
---
# <a name="ndis-60-design-objectives"></a>NDIS 6.0 の設計目標





2 つの主な目標が設計と NDIS 6.0 の開発をガイドします。

1.  ドライバーのパフォーマンスとスケーラビリティを強化します。 (を参照してください[強化されたパフォーマンスとスケーラビリティ](enhanced-performance-and-scalability.md)詳細についてはします)。

    次のように主要な機能強化は、クライアントとサーバーの両方のパフォーマンスが著しく向上を提供します。

    -   ネットワーク データのパッケージ化
    -   送信し、受信パス
    -   実行時の再構成機能
    -   DMA のスキャッター/ギャザー
    -   フィルター ドライバー
    -   受信したデータ処理のマルチプロセッサのスケーリング
    -   Nic にオフロードすることの TCP タスク

2.  NDIS ドライバー モデルを簡略化します。 (を参照してください[ドライバー モデルの簡略化された](simplified-driver-model.md)詳細についてはします)。

    次の機能強化は、ドライバーの開発を簡略化します。

    -   簡素化されたドライバーの初期化
    -   NDIS インターフェイスのバージョン管理サポート
    -   簡略化されたリセット処理
    -   管理情報を取得するための標準インターフェイス
    -   中間のフィルター ドライバーを置換するフィルター ドライバー モデル

 

 






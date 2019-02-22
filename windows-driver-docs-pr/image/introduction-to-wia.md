---
title: WIA の概要
description: WIA の概要
ms.assetid: 51674b06-f9d5-4e35-a2ec-9d6cc0a09ef3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74947d485e7667bd185c6fa4a0db3f2c14da1b9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529980"
---
# <a name="introduction-to-wia"></a>WIA の概要





Microsoft Windows Image Acquisition (WIA) インターフェイスには、アプリケーション プログラミング インターフェイス (API) とデバイス ドライバー インターフェイス (DDI) の両方です。 WIA API を許可するのには設計されています。

-   信頼性の高い安定した環境で実行します。

-   相互運用性の問題を最小限に抑えます。

-   使用可能なイメージの取得のデバイスを列挙します。

-   同時に複数のデバイスへの接続を作成します。

-   標準および拡張可能な方法では、デバイスのプロパティを照会します。

-   標準と高パフォーマンスの転送メカニズムを使用してデバイスのデータを取得します。

-   データ転送の間には、画像のプロパティを維持します。

-   さまざまなデバイスのイベントの通知。

個々 のソリューションを作成する柔軟性を維持しながら、ハードウェア ベンダーが作成する必要がありますコードの量を最小限に抑えるには、WIA DDI は設計されています。 これは、によって実現されます。

-   ほとんどのドライバー操作を実行する標準的なデバイス サービス ライブラリを提供します。

-   業界デバイス通信規格をなど、画像転送プロトコル (PTP)、昇格するため 1 つ WIA ドライバーほとんど WIA デバイス サポートします。

このセクションでは、次の領域における WIA の簡単な概要では。

[WIA アーキテクチャの概要](wia-architecture-overview.md)

[WIA コア コンポーネント](wia-core-components.md)

 

 





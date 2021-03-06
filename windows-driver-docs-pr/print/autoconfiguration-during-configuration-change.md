---
title: 構成変更時の自動構成
description: 構成変更時の自動構成
ms.assetid: 0294d34d-06e4-4e57-8f4d-4100ab482852
keywords:
- 構成の変更時に、自動構成の WDK プリンター
- 構成の変更時に、プリンターの自動構成の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd3e878dbd482c0ba72504ef97438c9a2cecb38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370505"
---
# <a name="autoconfiguration-during-configuration-change"></a>構成変更時の自動構成


デバイスがインストールされた後、ポート モニターがイベントを送信することによって、またはポーリングによって、構成データを最新に保つ責任を負います。 ドライバーまたはアプリケーションがデバイスの現在の構成に関心がある、ときに使用できる、[双方向の通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)と[双方向通信スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)ポート モニターにクエリを実行するにはこの情報。

次の図は、デバイスの構成が変更されたときの自動構成で、データ フローを示します。

![デバイスの構成が変更されたときに、自動構成内のデータ フローを示す図](images/autocfgcfgchange.png)

1.  デバイスの構成が変更されたときに、Web サービスのイベント (Ws-eventing) プロトコルを使用するデバイスは、その状態が変化していますが、特定の変更については説明しません印刷サブシステムを通知します。 標準の TCP/IP ポート モニタは、Ws-eventing をサポートしていないデバイスをポーリングします。

2.  ポート モニターには、デバイスの構成が変更され、スプーラーに通知を送信する通知が生成されます。

3.  スプーラは、呼び出すことによって、ドライバーに通知を送信`DrvPrinterEvent`プリンターを渡すと\_イベント\_構成\_呼び出しで更新します。 この関数の呼び出しは、デバイスの構成が変更されたドライバーを通知するために機能します。

ドライバーは、通知メッセージは (スキーマは、双方向の通知デザイン仕様で定義されている) 変更された値を保持するために、デバイスの構成での変更がある場合を判断できます。 ただし、通知が大きすぎて通知メカニズムを経由して送信する場合、通知はそれぞれのデバイスの特性が変更されたことを示しますが、その新しい値の詳細なし、1 つ以上の ReducedSchema インスタンスがあります。

 

 





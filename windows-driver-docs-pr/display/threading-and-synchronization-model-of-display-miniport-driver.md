---
title: スレッド処理と表示のミニポート ドライバーのモデルの同期
description: スレッド処理と表示のミニポート ドライバーの同期モデル
ms.assetid: 4e5cf498-a2d1-44d5-b7a3-427f48b5da50
keywords:
- WDK の表示、ミニポート ドライバーをスレッド処理
- WDK の表示、ミニポート ドライバーの同期
- ミニポート ドライバー WDK ディスプレイ、同期
- スレッド処理、ミニポート ドライバー WDK を表示します。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 53da24251f21d6fa574d496fd91558b85b0085cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535616"
---
# <a name="threading-and-synchronization-model-of-display-miniport-driver"></a>スレッド処理と表示のミニポート ドライバーの同期モデル

複数のスレッドを同時にディスプレイのミニポート ドライバー内に存在することはできます。 これは一般に、ディスプレイのミニポート ドライバーがある再入可能です。 ただし、一部の呼び出し、ディスプレイのミニポート ドライバーをすることはできません再入可能か、グラフィックス ハードウェアまたはアクセスのスレッド間のグローバルなデータ構造体にアクセスするためです。 再入または nonreentrancy は呼び出しごとのレベルで選択することはできません、Windows Display Driver Model (WDDM) 事前代入すると、1 回の呼び出しを正確にドライバーが期待どおりの呼び出しを定義する次の同期レベル。

-   [スレッド処理と 3 番目のレベルの同期](threading-and-synchronization-third-level.md)

-   [スレッド処理と第 2 レベルの同期](threading-and-synchronization-second-level.md)

-   [スレッド処理との同期の最初のレベル](threading-and-synchronization-first-level.md)

-   [スレッド処理と同期 0 レベル](threading-and-synchronization-zero-level.md)

-   [スレッドの同期と TDR](thread-synchronization-and-tdr.md)

 

 






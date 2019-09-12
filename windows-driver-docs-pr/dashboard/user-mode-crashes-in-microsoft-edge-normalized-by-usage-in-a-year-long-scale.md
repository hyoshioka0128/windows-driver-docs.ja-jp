---
title: Microsoft Edge でのユーザー モード クラッシュのユーザーの数
description: この測定値は、年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft Edge のクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: aee8c2b7387c0aeead4faee7c17c80829f2e94c2
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223882"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-microsoft-edge-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>Microsoft Edge におけるユーザー モードの信頼性を示すクラッシュ数を使用量で正規化した値がベースライン目標と同じかそれより小さい

## <a name="description"></a>説明

ユーザーが Microsoft Edge を使用してインターネットを参照する際、Web からの視覚的データがグラフィックス コンポーネントによって処理されて、レンダリングされたビューがユーザーの画面に表示されます。 この測定値は、当該のドライバーがインストールされているすべてのデバイス上で、Microsoft Edge がクラッシュする頻度を、Microsoft Edge の実行時間の観点から監視するものです。 Microsoft Edge がクラッシュした場合、再び使用できる状態になるまで、ユーザーはそのアプリケーションの回復を待機する必要があります。

この測定値は、1 年間の使用量で正規化されます。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|50,000 時間 (Microsoft Edge の実行時間)|
|**合格基準**|実行時のクラッシュが 1 年間に 1 回以下|
|**測定 ID**|17377831|

## <a name="calculation"></a>計算

1. この測定値は、**年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft Edge のクラッシュの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
2. "*Microsoft Edge の総クラッシュ回数 = ドライバーがインストールされているマシンで Microsoft Edge がクラッシュした回数*"
3. "*Microsoft Edge の総実行時間 = ドライバーがインストールされている各マシンにおける Microsoft Edge の実行時間の合計*"
4. "*年間実行時間 = Microsoft Edge の総実行時間 \* 60 (分) \* 60 (時間) \* 24 (日) \* 365 (年)* "

### <a name="final-calculation"></a>最終的な計算

"*使用量で正規化した Microsoft Edge のクラッシュ回数 = Microsoft Edge の総クラッシュ回数 / 年間実行時間*"
---
title: 使用量により正規化された Microsoft Edge Chromium でのユーザー モード クラッシュの数 <= ベースライン目標
description: この測定値は、年換算の総実行時間について、グラフィックス ドライバーに起因する Microsoft Edge Chromium のクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: fc29cadf3169339ab03b485516729ddcd66162d6
ms.sourcegitcommit: d7b5e6049db3109fdcbe83279875f24f3fa6acdd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84110240"
---
# <a name="number-of-user-mode-crashes-in-microsoft-edge-chromium-normalized-by-usage--baseline-goal"></a>使用量により正規化された Microsoft Edge Chromium でのユーザー モード クラッシュの数 <= ベースライン目標

## <a name="description"></a>説明

ユーザーが Edge Chromium を使用してインターネットを参照する際、Web からの視覚的データがグラフィックス コンポーネントによって処理されて、レンダリングされたビューがユーザーの画面に表示されます。 この測定値は、当該のドライバーがインストールされているすべてのデバイス上で、Edge Chromium がクラッシュする頻度を、Edge Chromium の実行時間の観点から監視するものです。 Edge Chromium がクラッシュした場合、再び使用できる状態になるまで、ユーザーはそのアプリケーションの回復を待機する必要があります。  

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|ドライバーの対象となるデバイス|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|30,000 時間 (Microsoft Edge Chromium の実行時間)|
|**合格基準**|<= 1 年あたり 1 クラッシュ|
|**測定 ID**|25481659|

## <a name="calculation"></a>計算

この測定値は、年換算の総実行時間について、グラフィックス ドライバーに起因する Microsoft Edge Chromium のクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです

Edge Chromium の総クラッシュ = ドライバーがインストールされているマシンで Edge Chromium がクラッシュした回数

Edge Chromium の総実行時間 = ドライバーがインストールされている各マシンにおける Edge Chromium の実行時間の合計

年換算の実行時間 = Edge Chromium 総実行時間 ∗ 60 (分) ∗ 60 (時間) ∗ 24 (日) ∗ 365 (年)

### <a name="final-calculation"></a>最終的な計算

使用量 = Edge Chromium の総クラッシュ回数/年間実行時間で正規化した Edge Chromium のクラッシュ回数

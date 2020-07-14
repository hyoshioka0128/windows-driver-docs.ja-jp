---
title: 使用量により正規化された Microsoft Edge Chromium でのユーザー モード クラッシュの数 <= ベースライン目標
description: この測定値は、年換算の総実行時間について、グラフィックス ドライバーに起因する Microsoft Edge Chromium のクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: d1602b18df3d073bb586b52562d58beb4048f9e6
ms.sourcegitcommit: cb5f370b867ceab28b6b6c64a3586b0bb3831b3d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86036022"
---
# <a name="number-of-user-mode-crashes-in-microsoft-edge-chromium-normalized-by-usage--baseline-goal-ecosystem"></a>使用量により正規化された Microsoft Edge Chromium でのユーザー モード クラッシュの数 <= ベースライン目標 (エコシステム)

## <a name="description"></a>説明

ユーザーが Edge Chromium を使用してインターネットを参照する際、Web からの視覚的データがグラフィックス コンポーネントによって処理されて、レンダリングされたビューがユーザーの画面に表示されます。 この測定値は、当該のドライバーがインストールされているすべてのデバイス上で、Edge Chromium がクラッシュする頻度を、Edge Chromium の実行時間の観点から監視するものです。 Edge Chromium がクラッシュした場合、再び使用できる状態になるまで、ユーザーはそのアプリケーションの回復を待機する必要があります。  

これは、[Microsoft Edge Chromium での使用量により正規化されたユーザー モードのクラッシュ数 <= ベースライン目標](https://docs.microsoft.com/windows-hardware/drivers/dashboard/graphics-user-mode-crashes-edge-chromium-standard)の測定値のエコシステムに対応するものです。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|エコシステム|
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

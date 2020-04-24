---
title: Microsoft のトップ アプリでのユーザー モード クラッシュの数
description: この測定値は、年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft のトップ アプリのクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e105afa17077bdbacd9e5c95c14777a0987d50a9
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71016966"
---
# <a name="number-of-user-mode-crashes-in-top-microsoft-apps-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>Microsoft のトップ アプリにおけるユーザー モード クラッシュ数を使用量で正規化した値がベースライン目標と同じかそれより小さい

## <a name="description"></a>説明

ユーザーがアプリケーションを開いて使用する際、アプリの視覚的情報がグラフィックス コンポーネントによって処理されて、レンダリングされたビューがユーザーの画面に表示されます。 この測定値は、当該のドライバーがインストールされているすべてのデバイス上で、Microsoft のトップ アプリがクラッシュする頻度を、それらのアプリケーションの実行時間の観点から監視するものです。 アプリケーションがクラッシュした場合、再び使用できる状態になるまで、ユーザーはその回復を待機する必要があります。

この測定値は、1 年間の使用量で正規化されます。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|100,000 時間 (Microsoft のトップ アプリの実行時間)|
|**合格基準**|実行時のクラッシュが 1 年間に 1.5 回以下|
|**測定 ID**|17377268|

## <a name="calculation"></a>計算

1. この測定値は、**年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft のトップ アプリのクラッシュの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*Microsoft のトップ アプリの総クラッシュ回数 = ドライバーがインストールされているマシンで Microsoft のトップ アプリがクラッシュした回数*"
3. "*Microsoft のトップ アプリの総実行時間 = ドライバーがインストールされている各マシンにおける Microsoft のトップ アプリの実行時間の合計*"
4. *年間実行時間 = Microsoft のトップ アプリの総実行時間 \* 60 (分) \* 60 (時間) \* 24 (日) \* 365 (年)*

### <a name="final-calculation"></a>最終的な計算

*使用量で正規化した Microsoft のトップ アプリにおけるクラッシュ回数 = Microsoft のトップ アプリの総クラッシュ回数 / 年間実行時間*
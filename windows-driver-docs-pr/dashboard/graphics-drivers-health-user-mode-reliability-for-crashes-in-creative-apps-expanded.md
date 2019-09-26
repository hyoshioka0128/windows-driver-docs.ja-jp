---
title: クリエイティブ アプリケーションにおけるユーザー モードの信頼性を示すクラッシュ数
description: この測定値は、年単位の総実行時間について、グラフィックス ドライバーに起因するクリエイティブ アプリケーションのクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 00c88187a857cfc107189f317249ba5dd5f23612
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017066"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-creative-applications-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>クリエイティブ アプリケーションにおけるユーザー モードの信頼性を示すクラッシュ数を使用量で正規化した値がベースライン目標と同じかそれより小さい

## <a name="description"></a>説明

この測定値では、クリエイティブ アプリケーションのコンテキスト内で発生したディスプレイ ドライバーのクラッシュの数をカウントし、更新されたドライバーがインストールされているすべてのマシンにおける[クリエイティブ アプリケーション](measure-appendix.md#creative-applications-example)の実行時間を計算します。 その後、総実行時間を年単位に正規化して、ユーザーがクリエイティブ アプリケーションを 1 年間使用した場合に発生するクラッシュの数を示します。

この測定値を使用量で正規化した値が、ベースライン目標と同じかそれを下回る必要があります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|展開|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|1,000 時間 (クリエイティブ アプリケーションの実行時間)|
|**合格基準**|実行時のクラッシュが 1 年間に 10 回以下|
|**測定 ID**|22843595|

## <a name="calculation"></a>計算

1. この測定値は、**年単位の総実行時間について、グラフィックス ドライバーに起因するクリエイティブ アプリケーションのクラッシュの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*クリエイティブ アプリケーションの総クラッシュ回数 = ドライバーがインストールされているマシンでクリエイティブ アプリケーションがクラッシュした回数*"
3. "*クリエイティブ アプリケーションの総実行時間 = ドライバーがインストールされている各マシンにおけるクリエイティブ アプリケーションの実行時間の合計*"
4. "*年間実行時間 = クリエイティブ アプリケーションの総実行時間 \* 60 (分) \* 60 (時間) \* 24 (日) \* 365 (年)* "

### <a name="final-calculation"></a>最終的な計算

"*年単位の使用量で正規化したクリエイティブ アプリケーションのクラッシュ回数 = クリエイティブ アプリケーションの総クラッシュ回数 / 年間実行時間*"
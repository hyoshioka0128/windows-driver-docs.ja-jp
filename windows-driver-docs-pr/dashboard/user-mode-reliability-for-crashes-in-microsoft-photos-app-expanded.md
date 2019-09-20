---
title: Microsoft フォト アプリにおけるユーザー モードの信頼性を示すクラッシュ数がベースライン目標と同じかそれより小さい
description: この測定値は、年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft フォトのクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 08/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 762a85c8e3064d200ce7e1f61b932ba1647eedf9
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016992"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-microsoft-photos-app-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal"></a>Microsoft フォト アプリにおけるユーザー モードの信頼性を示すクラッシュ数を使用量で正規化した値がベースライン目標と同じかそれより小さい

## <a name="description"></a>説明

この測定値では、Microsoft フォト アプリケーションのコンテキスト内で発生したディスプレイ ドライバーのクラッシュの数をカウントし、更新されたドライバーがインストールされているすべてのマシンにおける Microsoft フォトの実行時間を計算します。 その後、総実行時間を年単位に正規化して、ユーザーが Microsoft フォトを 1 年間使用した場合に発生するクラッシュの数を示します。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|展開|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小インスタンス**|10,000 時間 (Microsoft フォトの実行時間) |
|**合格基準**|実行時のクラッシュが 1 年間に 1.5 回以下|
|**測定 ID**|22726049|

## <a name="calculation"></a>計算

1. この測定値は、**年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft フォトのクラッシュの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*Microsoft フォト アプリの総クラッシュ回数 = ドライバーがインストールされているマシンで Microsoft フォトがクラッシュした回数*"
3. "*Microsoft フォトの総実行時間 = ドライバーがインストールされている各マシンにおける Microsoft フォトの実行時間の合計*"
4. "*年間実行時間 = Microsoft フォトの総実行時間 \* 60 (分) \* 60 (時間) \* 24 (日) \* 365 (年)* "

### <a name="final-calculation"></a>最終的な計算

"*年単位の使用量で正規化した Microsoft フォトのクラッシュ回数 = Microsoft フォトの総クラッシュ回数 / 年間実行時間*"

---
title: Microsoft フォト アプリにおけるユーザー モードの信頼性を示すクラッシュ数がベースライン目標と同じかそれより小さい
description: この測定値は、年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft フォトのクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: d7c455b0240feb1445fab05d347bdaf0d8034787
ms.sourcegitcommit: cb5f370b867ceab28b6b6c64a3586b0bb3831b3d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86036024"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-microsoft-photos-app-normalized-by-usage-is-less-than-or-equal-to-the-baseline-goal-ecosystem"></a>Microsoft フォト アプリにおけるユーザー モードの信頼性を示すクラッシュ数を使用量で正規化した値が、ベースライン目標と同じかそれより小さい (エコシステム)

## <a name="description"></a>説明

この測定値では、Microsoft フォト アプリケーションのコンテキスト内で発生したディスプレイ ドライバーのクラッシュの数をカウントし、更新されたドライバーがインストールされているすべてのマシンにおける Microsoft フォトの実行時間を計算します。 その後、総実行時間を年単位に正規化して、ユーザーが Microsoft フォトを 1 年間使用した場合に発生するクラッシュの数を示します。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小インスタンス**|10,000 時間 (Microsoft フォトの実行時間) |
|**合格基準**|実行時のクラッシュが 1 年間に 1.5 回以下|
|**測定 ID**|20240794|

## <a name="calculation"></a>計算

1. この測定値は、**年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft フォトのクラッシュの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*Microsoft フォト アプリの総クラッシュ回数 = ドライバーがインストールされているマシンで Microsoft フォトがクラッシュした回数*"
3. "*Microsoft フォトの総実行時間 = ドライバーがインストールされている各マシンにおける Microsoft フォトの実行時間の合計*"
4. "*年間実行時間 = Microsoft フォトの総実行時間 \* 60 (分) \* 60 (時間) \* 24 (日) \* 365 (年)* "

### <a name="final-calculation"></a>最終的な計算

"*年単位の使用量で正規化した Microsoft フォトのクラッシュ回数 = Microsoft フォトの総クラッシュ回数 / 年間実行時間*"

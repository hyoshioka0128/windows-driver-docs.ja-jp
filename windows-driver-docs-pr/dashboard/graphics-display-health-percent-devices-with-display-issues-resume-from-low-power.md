---
title: 低電力状態からの再開時に表示の問題が発生したマシンの割合
description: この測定値は、低電力状態からの再開時に表示の問題が発生したマシンの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: afff2ace99951da7649aa8037b98fe7434fd17eb
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70224022"
---
# <a name="percent-of-machines-with-display-issues-when-resume-from-low-power-state"></a>低電力状態からの再開時に表示の問題が発生したマシンの割合

## <a name="description"></a>説明

低電力状態からマシンが起動する際に、グラフィックス コンポーネントのエラーによって、ユーザーのエクスペリエンスに影響を及ぼす表示の問題が発生する場合があります。 この測定値では、低電力状態からの再開時に表示の問題が発生したマシンの割合を計算します。 表示の問題の一覧については、[付録](measure-appendix.md#display-issues)を参照してください。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|低電力状態だった 100 台のマシン|
|**合格基準**|低電力状態のマシンのうち、表示の問題が発生する割合が 0.8% 以下|
|**測定 ID**|19920755|

## <a name="calculation"></a>計算

1. この測定値は、**低電力状態からの再開時に表示の問題が発生したマシンの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*表示の問題が起こったマシンの数 = 低電力状態からの再開時に表示の問題が発生したマシンの数*"
3. "*マシンの総数 = フライト中に低電力状態から高電力状態への遷移が行われたマシンの数*"

### <a name="final-calculation"></a>最終的な計算

"*低電力状態からの再開時に表示の問題が発生したマシンの割合 = 表示の問題が起こったマシンの数 / マシンの総数*"

---
title: subpar ストリーム初期化成功率のあるマシンの割合
description: この測定値は、subpar 初期化率のあるマシンの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 9dde8d724e9a34a772941f00fced39901688b1ca
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223906"
---
# <a name="percent-of-machines-with-subpar-stream-initialization-success-rate"></a>subpar ストリーム初期化成功率のあるマシンの割合

## <a name="description"></a>説明

この測定値では、各マシンの "*初期化成功率*" を特定し、ストリーム初期化率が 90% 未満のマシンの割合を計算します。 デバイスがオーディオ ストリームを初期化できない場合、ユーザーはアプリケーションのオーディオ エクスペリエンスにアクセスできません。 

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日|
|**測定基準**|マシンの集計|
|**最小母集団**|50 台のマシン|
|**合格基準**|初期化成功率が 90% 未満のマシンが 1% 以下 |
|**測定 ID**|11458866|

## <a name="calculation"></a>計算

1. この測定値は、**subpar 初期化率のあるマシンの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*マシンごとに、次のように計算します。* "

   a. "*マシンの初期化成功率 = 初期化の失敗回数 / 初期化の合計試行回数*"

   b. "*失敗したマシン = マシンの初期化成功率が 90% 未満*"

3. "*subpar 初期化が行われたマシンの台数 = 失敗したマシンの台数*"
4. "*総マシン数 = 初期化を試行したすべてのマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*subpar 初期化率のあるマシンの割合 = subpar 初期化が行われたマシンの台数 / 総マシン数*"

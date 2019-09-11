---
title: 少なくとも 1 つのオーディオ ストリーム初期化エラーが発生したマシンの割合
description: この測定値は、予期しない初期化エラーが少なくとも 1 つ発生したマシンの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: 0f90e511c755ff8e9b8bfefd641adeb982b85496
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70223942"
---
# <a name="percent-of-machines-with-at-least-one-audio-stream-initialization-failure"></a>少なくとも 1 つのオーディオ ストリーム初期化エラーが発生したマシンの割合

## <a name="description"></a>説明

デバイスがオーディオ ストリームを初期化できない場合、ユーザーはアプリケーションのオーディオ エクスペリエンスにアクセスできません。 この測定値は、オーディオ デバイスがストリームを初期化できなかったマシンの割合を計算したものです。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|50 台のマシン|
|**合格基準**|少なくとも 1 つのオーディオ ストリーム初期化エラーが発生したマシンが 8% 以下|
|**測定 ID**|12111510|

## <a name="calculation"></a>計算

1. この測定値は、**予期しない初期化エラーが少なくとも 1 つ発生したマシンの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
2. "*初期化エラーが発生したマシンの台数 = 予期しない初期化エラーが少なくとも 1 つ発生したマシンの台数*"
3. "*総マシン数 = オーディオ ストリームの初期化を試行したマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*少なくとも 1 つのストリーム初期化エラーが発生したマシンの割合 = 初期化エラーが発生したマシンの台数 / 総マシン数*"

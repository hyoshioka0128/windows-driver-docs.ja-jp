---
title: 少なくとも 1 つのオーディオ ストリーム初期化エラーが発生したマシンの割合
description: この測定値は、予期しない初期化エラーが少なくとも 1 つ発生したマシンの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1c67e56efcc044c7aebe7840a450581a233daa7f
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71195763"
---
# <a name="percent-of-machines-with-at-least-one-audio-stream-initialization-failure"></a>少なくとも 1 つのオーディオ ストリーム初期化エラーが発生したマシンの割合

## <a name="description"></a>説明

[オーディオの測定値](audio-measures.md)の「オーディオ ストリームの初期化」セクションを参照してください

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard|
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

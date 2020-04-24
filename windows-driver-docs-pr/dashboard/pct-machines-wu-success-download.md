---
title: 過去 28 日以内に WU がダウンロードの成功を報告したマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、Windows Update からダウンロードの成功が報告されたマシンの割合に集計したものです
ms.topic: article
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: ee75ce1be42905004068ced6bfefedea6967a1e5
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "79083190"
---
# <a name="percent-of-machines-that-wu-reported-a-successful-download-within-the-last-28-days"></a>過去 28 日以内に WU がダウンロードの成功を報告したマシンの割合

## <a name="description"></a>説明

過去 28 日以内に WU がダウンロードの成功を報告したマシンの割合

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|100|
|**合格基準**|95% 以上|
|**測定 ID**|24186432|

## <a name="calculation"></a>計算

WU がダウンロードの成功を報告したマシンの数 (status == 0) / 

WU のダウンロードを試行したマシンの数

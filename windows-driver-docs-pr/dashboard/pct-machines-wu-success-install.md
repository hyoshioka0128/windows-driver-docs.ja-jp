---
title: 過去 28 日以内に WU がインストールの成功を報告したマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、Windows Update からインストールの成功が報告されたマシンの割合に集計したものです
ms.topic: article
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2b68b3037cfb77e5d7d66cada1284b04c77ac876
ms.sourcegitcommit: 387de60712790691970924e059b0564325e211bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79083192"
---
# <a name="percent-of-machines-that-wu-reported-a-successful-installation-within-the-last-28-days"></a>過去 28 日以内に WU がインストールの成功を報告したマシンの割合

## <a name="description"></a>説明

過去 28 日以内に WU がインストールの成功を報告したマシンの割合

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|100|
|**合格基準**|95% 以上|
|**測定 ID**|24185194|

## <a name="calculation"></a>計算

WU がインストールの成功を報告したマシンの数 (status == 0) / 

WU のインストールを試行したマシンの数

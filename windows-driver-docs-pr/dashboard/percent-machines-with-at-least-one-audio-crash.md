---
title: 少なくとも 1 つのオーディオ クラッシュが発生したマシンの割合
description: この測定値は、AudioSrv.dll または AudioDG.exe でオーディオ クラッシュが少なくとも 1 回発生したマシンの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 99e2dcf9c93e10c6aa08b0f565f08e273568346e
ms.sourcegitcommit: 9f6f7d9e327ac3bd34643d8b062e11958a0fe05f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2019
ms.locfileid: "71195759"
---
# <a name="percent-of-machines-with-at-least-one-audio-crash"></a>少なくとも 1 つのオーディオ クラッシュが発生したマシンの割合

## <a name="description"></a>説明

[オーディオの測定値](audio-measures.md)の「オーディオ ユーザーモードの信頼性」セクションを参照してください

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|毎日 (7 日間の平均)|
|**測定基準**|マシンの割合|
|**最小母集団**|動的 (信頼区間を使用)|
|**合格基準**|AudioSrv でクラッシュが少なくとも 1 回発生したマシンが 0.4% 以下<br/>AudioSrv または AudioDG でクラッシュが少なくとも 1 回発生したマシンが 1% 未満|
|**測定 ID**|12518948 - AudioSrv のみ<br/>23032999 - AudioSrv と AudioDG の両方|

## <a name="calculation"></a>計算

毎日:
1. AudioSrv または AudioDg でクラッシュしたマシンの数をカウントします
1. オーディオを使用しようとしたマシンの数をカウントします
1. クラッシュしたマシンの割合 = (クラッシュが発生したマシンの数) / (オーディオを使用しようとしたマシンの数)

測定値の値は、常にこの割合の 7 日間のローリング平均になります。
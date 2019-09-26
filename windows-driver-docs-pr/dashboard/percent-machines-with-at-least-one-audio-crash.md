---
title: 少なくとも 1 つのオーディオ クラッシュが発生したマシンの割合
description: この測定値は、AudioSrv.dll または AudioDG.exe でオーディオ クラッシュが少なくとも 1 回発生したマシンの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 430e618fa9c75d9b5e56480b4cf4c2283d540513
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016941"
---
# <a name="percent-of-machines-with-at-least-one-audio-crash"></a>少なくとも 1 つのオーディオ クラッシュが発生したマシンの割合

## <a name="description"></a>説明

この測定値は、"*Windows オーディオ サービス (AudioSrv.dll)* " と "*オーディオ デバイス グラフ (AudioDG.exe)* " という 2 つのサービスを監視して、どちらかのサービスでクラッシュが発生したかどうかを確認するものです。 どちらかのサービスがクラッシュした場合、ユーザーのマシンはオーディオを再生できず、ユーザーはサービスが回復して、オーディオ ストリームが再初期化されるまで待機する必要があります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日|
|**測定基準**|マシンの割合|
|**最小母集団**|50 台のマシン|
|**合格基準**|どちらかのオーディオ サービスでクラッシュが少なくとも 1 回発生したマシンが 0.4% 以下|
|**測定 ID**|12518948|

## <a name="calculation"></a>計算

1. この測定値は、**AudioSrv.dll または AudioDG.exe でオーディオ クラッシュが少なくとも 1 回発生したマシンの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
2. "*クラッシュが発生したマシンの台数 = AudioSrv.dll または AudioDG.exe でクラッシュが少なくとも 1 回発生したマシンの台数*"
3. "*総マシン数 = 少なくとも 1 つのオーディオ ストリームが正常に初期化されたマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*オーディオ クラッシュが少なくとも 1 回発生したデバイスの割合 = クラッシュが発生したマシンの台数 / 総マシン数*"
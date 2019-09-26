---
title: 少なくとも 1 つのオーディオ ハングが発生したマシンの割合
description: この測定値は、AudioSrv.dll または AudioDG.exe でオーディオ ハングが少なくとも 1 回発生したマシンの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: f8cd5ab85577f712b70c5e94bc56417e83e7d040
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017024"
---
# <a name="percent-of-machines-with-at-least-one-audio-hang"></a>少なくとも 1 つのオーディオ ハングが発生したマシンの割合

## <a name="description"></a>説明

この測定値は、"*Windows オーディオ サービス (AudioSrv.dll)* " と "*オーディオ デバイス グラフ (AudioDG.exe)* " という 2 つのサービスを監視して、どちらかのサービスでハングが発生したかどうかを確認するものです。 オーディオがハングすると、オーディオ プラットフォームがユーザー アプリケーションに応答しなくなります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日|
|**測定基準**|マシンの集計|
|**最小母集団**|50 台のマシン|
|**合格基準**|どちらかのオーディオ サービスでハングが少なくとも 1 回発生したマシンが 1.3% 以下|
|**測定 ID**|11458540|

## <a name="calculation"></a>計算

1. この測定値は、**AudioSrv.dll または AudioDG.exe でオーディオ ハングが少なくとも 1 回発生したマシンの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*ハングが発生したマシンの台数 = AudioSrv.dll または AudioDG.exe でハングが少なくとも 1 回発生したマシンの台数*"
3. "*総マシン数 = 少なくとも 1 つのオーディオ ストリームが正常に初期化されたマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*オーディオ ハングが少なくとも 1 回発生したマシンの割合 = ハングが発生したマシンの台数 / 総マシン数*"
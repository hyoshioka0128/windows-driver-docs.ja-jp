---
title: KSNODETYPE\_イコライザー
description: KSNODETYPE\_イコライザー
ms.assetid: 03812936-57ba-4762-b716-858b7f14908f
keywords:
- KSNODETYPE_EQUALIZER オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_EQUALIZER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566c2d5eb58377f0c39a5afa2a789c97b74ed044
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551041"
---
# <a name="ksnodetypeequalizer"></a>KSNODETYPE\_イコライザー


## <span id="ddk_ksnodetype_equalizer_ks"></span><span id="DDK_KSNODETYPE_EQUALIZER_KS"></span>


KSNODETYPE\_イコライザーのノードは、イコライザーの複数の頻度バンドとを表します。 イコライゼーション テーブルに割り当てます周波数バンドの各レベルを調整することによって、EQ ノードはノードの出力ストリームに表示される各周波数バンドの量を制御できます。

EQ、ノードが 1 つの入力ストリームと 1 つの出力ストリームに 2 つのストリームは、一般的なデータ形式を共有します。

KSNODETYPE\_イコライザーのノードは、次の必須プロパティをサポートする必要があります。

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

 

 






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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333207"
---
# <a name="ksnodetypeequalizer"></a>KSNODETYPE\_イコライザー


## <span id="ddk_ksnodetype_equalizer_ks"></span><span id="DDK_KSNODETYPE_EQUALIZER_KS"></span>


KSNODETYPE\_イコライザーのノードは、イコライザーの複数の頻度バンドとを表します。 イコライゼーション テーブルに割り当てます周波数バンドの各レベルを調整することによって、EQ ノードはノードの出力ストリームに表示される各周波数バンドの量を制御できます。

EQ、ノードが 1 つの入力ストリームと 1 つの出力ストリームに 2 つのストリームは、一般的なデータ形式を共有します。

KSNODETYPE\_イコライザーのノードは、次の必須プロパティをサポートする必要があります。

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

 

 






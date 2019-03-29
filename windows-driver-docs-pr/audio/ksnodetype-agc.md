---
title: KSNODETYPE\_AGC
description: KSNODETYPE\_AGC
ms.assetid: 54d6bb6a-9c15-4020-bc6e-92b24878e1fd
keywords:
- KSNODETYPE_AGC オーディオ デバイス
topic_type:
- apiref
api_name:
- KSNODETYPE_AGC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2676a77bb38cb5aa79a11198112f34d0eb8e47b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574271"
---
# <a name="ksnodetypeagc"></a>KSNODETYPE\_AGC


## <span id="ddk_ksnodetype_agc_ks"></span><span id="DDK_KSNODETYPE_AGC_KS"></span>


KSNODETYPE\_AGC ノードは、自動ゲイン制御 (AGC) を表します。 AGC ノードが 1 つの入力ストリームと 1 つの出力ストリームの 2 つのストリームは、同じデータ形式。 ノードには、減衰したり、信号をクリッピングすることがなく最大のダイナミック レンジを実現するために入力ストリームに適用される量が自動的に調整されます。

KSNODETYPE\_AGC ノードは、次のプロパティをサポートする必要があります。

[**KSPROPERTY\_オーディオ\_AGC**](ksproperty-audio-agc.md)

KSNODETYPE\_AGC ノードは、次の省略可能なプロパティもサポートできます。

[**KSPROPERTY\_TOPOLOGYNODE\_を有効にします。**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_リセット**](ksproperty-topologynode-reset.md)

KSPROPERTY\_TOPOLOGYNODE\_両方を有効にして、ノードを無効に有効にするプロパティを使用します。 ノードはパススルー モードで動作を無効にした場合 (変更なしの出力に渡す入力ストリームを許可、)。

 

 






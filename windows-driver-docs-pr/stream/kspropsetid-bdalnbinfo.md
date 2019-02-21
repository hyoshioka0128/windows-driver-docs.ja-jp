---
title: KSPROPSETID\_BdaLNBInfo
description: KSPROPSETID\_BdaLNBInfo
ms.assetid: 2b385e93-2d0d-44ca-9cfc-58afea946db6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24f1049488fbdeeb88420332f7b8dfdf369b227e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549021"
---
# <a name="kspropsetidbdalnbinfo"></a>KSPROPSETID\_BdaLNBInfo


## <span id="ddk_kspropsetid_bdalnbinfo_ks"></span><span id="DDK_KSPROPSETID_BDALNBINFO_KS"></span>


KSPROPSETID\_BdaLNBInfo は BDA 低ノイズ ブロック (LNB) 情報プロパティ セット。 衛星通信の LNB デバイスに関する情報が、RF チューナーの提供に使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_LNB_LOF_LOW_BAND"></span><span id="ksproperty_bda_lnb_lof_low_band"></span>[**KSPROPERTY\_BDA\_LNB\_LOF\_低\_バンド**](ksproperty-bda-lnb-lof-low-band.md)  
低帯域 RF 信号の受信の頻度を移行する、LNB によって使用されるローカル オシレーター頻度 (LOF) については、RF チューナーのノードを通知します。

<span id="KSPROPERTY_BDA_LNB_LOF_HIGH_BAND"></span><span id="ksproperty_bda_lnb_lof_high_band"></span>[**KSPROPERTY\_BDA\_LNB\_LOF\_高\_バンド**](ksproperty-bda-lnb-lof-high-band.md)  
移行する高帯域 RF 信号の受信の頻度、LNB によって使用される LOF RF チューナーのノードを通知します。

<span id="KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY"></span><span id="ksproperty_bda_lnb_switch_frequency"></span>[**KSPROPERTY\_BDA\_LNB\_スイッチ\_頻度**](ksproperty-bda-lnb-switch-frequency.md)  
受信の RF 信号をチューナー位置から高帯域の LOF またはその逆を使用する低帯域 LOF を使用して切り替えるには、LNB デバイスに通知する必要がありますの頻度については、RF チューナーのノードを通知します。

### <a name="comments"></a>コメント

LNB は、衛星アンテナの中心点のデバイスです。 LNB は、アンテナによって反映される信号を収集し、RF チューナーの LNB アンプに送信します。

KSPROPSETID\_BdaLNBInfo プロパティ セットは、RF チューナーに衛星通信の LNB デバイスに関する情報を通信します。 クライアントが送信すると、 [ **KSPROPERTY\_BDA\_RF\_チューナー\_頻度**](ksproperty-bda-rf-tuner-frequency.md)チューナーが送信できる特定の頻度を RF チューナーをチューニングする要求で、必要な場合は、LNB のプロパティに従って、内部パラメーターを調整する LNB デバイスに信号を制御します。

### <a name="see-also"></a>参照

[**KSPROPERTY\_BDA\_RF\_チューナー\_頻度**](ksproperty-bda-rf-tuner-frequency.md)

 

 






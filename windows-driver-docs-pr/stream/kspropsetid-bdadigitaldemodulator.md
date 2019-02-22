---
title: KSPROPSETID\_BdaDigitalDemodulator
description: KSPROPSETID\_BdaDigitalDemodulator
ms.assetid: 536c247d-049b-4d48-96b7-f2aa01f1fa91
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab3c5945c68444e0134f383640a330368b52276f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530677"
---
# <a name="kspropsetidbdadigitaldemodulator"></a>KSPROPSETID\_BdaDigitalDemodulator


## <span id="ddk_kspropsetid_bdadigitaldemodulator_ks"></span><span id="DDK_KSPROPSETID_BDADIGITALDEMODULATOR_KS"></span>


KSPROPSETID\_BdaDigitalDemodulator は BDA デジタル復調器プロパティのセット。 設定する特定の値が必要な信号復調器ノードの制御に使用されます。

次のプロパティを使用できます。

<span id="KSPROPERTY_BDA_MODULATION_TYPE"></span><span id="ksproperty_bda_modulation_type"></span>[**KSPROPERTY\_BDA\_変調\_型**](ksproperty-bda-modulation-type.md)  
設定または QPSK など 8VSB 復調器の種類を取得します。

<span id="KSPROPERTY_BDA_INNER_FEC_TYPE"></span><span id="ksproperty_bda_inner_fec_type"></span>[**KSPROPERTY\_BDA\_内部\_FEC\_型**](ksproperty-bda-inner-fec-type.md)  
設定または内部の転送エラーの修正 (FEC) の種類を取得します。

<span id="KSPROPERTY_BDA_INNER_FEC_RATE"></span><span id="ksproperty_bda_inner_fec_rate"></span>[**KSPROPERTY\_BDA\_内部\_FEC\_率**](ksproperty-bda-inner-fec-rate.md)  
内部 FEC. で使用されるバイナリの畳み込みスキームを取得または設定

<span id="KSPROPERTY_BDA_OUTER_FEC_TYPE"></span><span id="ksproperty_bda_outer_fec_type"></span>[**KSPROPERTY\_BDA\_OUTER\_FEC\_型**](ksproperty-bda-outer-fec-type.md)  
設定または外部の FEC 型を取得します。

<span id="KSPROPERTY_BDA_OUTER_FEC_RATE"></span><span id="ksproperty_bda_outer_fec_rate"></span>[**KSPROPERTY\_BDA\_OUTER\_FEC\_率**](ksproperty-bda-outer-fec-rate.md)  
外部 FEC. で使用されるスキームをコーディング バイナリ明るさの値を取得または設定

<span id="KSPROPERTY_BDA_SYMBOL_RATE"></span><span id="ksproperty_bda_symbol_rate"></span>[**KSPROPERTY\_BDA\_シンボル\_率**](ksproperty-bda-symbol-rate.md)  
設定またはシンボルの率を取得します。

<span id="KSPROPERTY_BDA_SPECTRAL_INVERSION"></span><span id="ksproperty_bda_spectral_inversion"></span>[**KSPROPERTY\_BDA\_スペクトル\_逆転**](ksproperty-bda-spectral-inversion.md)  
設定またはスペクトルの逆転の設定を取得します。

<span id="KSPROPERTY_BDA_GUARD_INTERVAL"></span><span id="ksproperty_bda_guard_interval"></span>[**KSPROPERTY\_BDA\_GUARD\_間隔**](ksproperty-bda-guard-interval.md)  
設定または guard 間隔の設定値を取得します。

<span id="KSPROPERTY_BDA_TRANSMISSION_MODE"></span><span id="ksproperty_bda_transmission_mode"></span>[**KSPROPERTY\_BDA\_伝送\_モード**](ksproperty-bda-transmission-mode.md)  
設定または通知の送信ブロードキャストする方法の設定を取得します。

### <a name="comments"></a>コメント

KSPROPSETID\_BdaDigitalDemodulator プロパティ セットが DVB 復調器ノードのプロパティについて説明します。 KSPROPSETID ではなく、このプロパティを使用して\_BdaAutodemodulate、復調器が特定の値を設定する必要がある場合。

### <a name="see-also"></a>参照

[KSPROPSETID\_BdaAutodemodulate](kspropsetid-bdaautodemodulate.md)

 

 






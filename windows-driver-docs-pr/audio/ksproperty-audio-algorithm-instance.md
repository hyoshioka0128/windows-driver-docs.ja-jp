---
title: KSK プロパティ\_AUDIO\_ALGORITHM\_インスタンス
description: KSK プロパティ\_AUDIO\_ALGORITHM\_INSTANCE プロパティは、ノードがオーディオデータストリームに適用するサードパーティの効果を実現するために使用される、デジタル信号処理 (DSP) アルゴリズムを指定します。
ms.assetid: 8c27f856-de46-42a2-9f1f-e0cef1ee0f6e
keywords:
- KSPROPERTY_AUDIO_ALGORITHM_INSTANCE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_ALGORITHM_INSTANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362d6e8627474b4fa1a7518ed6a294648e5cbaff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831126"
---
# <a name="ksproperty_audio_algorithm_instance"></a>KSK プロパティ\_AUDIO\_ALGORITHM\_インスタンス


KSK プロパティ\_AUDIO\_ALGORITHM\_INSTANCE プロパティは、ノードがオーディオデータストリームに適用するサードパーティの効果を実現するために使用される、デジタル信号処理 (DSP) アルゴリズムを指定します。 このプロパティに対して定義されている効果には、音響エコー取り消しやノイズ抑制などがあります。

## <span id="ddk_ksproperty_audio_algorithm_instance_ks"></span><span id="DDK_KSPROPERTY_AUDIO_ALGORITHM_INSTANCE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、pin がそのデータストリームに適用される効果を識別する GUID です。 ヘッダーファイル Ksmedia. h の次の Guid のいずれかを指定できます。

<span id="KSALGORITHMINSTANCE_SYSTEM_AGC"></span><span id="ksalgorithminstance_system_agc"></span>KSALGORITHMINSTANCE\_SYSTEM\_AGC  
将来使用するために予約済み

<span id="KSALGORITHMINSTANCE_SYSTEM_ACOUSTIC_ECHO_CANCEL"></span><span id="ksalgorithminstance_system_acoustic_echo_cancel"></span>KSALGORITHMINSTANCE\_システム\_音響\_ECHO\_キャンセル  
システムの既定の音響エコーキャンセルアルゴリズム

<span id="KSALGORITHMINSTANCE_SYSTEM_MICROPHONE_ARRAY_PROCESSOR"></span><span id="ksalgorithminstance_system_microphone_array_processor"></span>KSALGORITHMINSTANCE\_システム\_マイク\_配列\_プロセッサ  
将来使用するために予約済み

<span id="KSALGORITHMINSTANCE_SYSTEM_NOISE_SUPPRESS"></span><span id="ksalgorithminstance_system_noise_suppress"></span>KSALGORITHMINSTANCE\_システム\_ノイズ\_抑制  
システムの既定のノイズ抑制アルゴリズム

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_ALGORITHM\_インスタンスプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティを使用して、AEC ノード ([**KSNODETYPE\_音響\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)) またはノイズ抑制ノード ([**KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md)) によって実行される DSP アルゴリズムを制御します。

アルゴリズムインスタンス GUID は、呼び出し元が**Idirectsoundcapture:: CreatecapDirectSoundFullDuplexCreate buffer**メソッドまたは関数に渡す、DSCEFFECTDESC 構造体の**guiddscfxinstance**メンバーの値と一致します. 詳細については、Microsoft Windows SDK のドキュメントを参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_音響\_ECHO\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md)

 

 







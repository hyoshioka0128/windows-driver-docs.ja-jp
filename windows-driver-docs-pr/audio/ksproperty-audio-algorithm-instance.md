---
title: KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス
description: KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス プロパティは、ノードがオーディオ データ ストリームに適用されるサード パーティ製の効果を実現するために使用されるデジタル信号処理 (DSP) アルゴリズムを指定します。
ms.assetid: 8c27f856-de46-42a2-9f1f-e0cef1ee0f6e
keywords:
- KSPROPERTY_AUDIO_ALGORITHM_INSTANCE オーディオ デバイス
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
ms.openlocfilehash: 22322c0c873ed2740e425bca61c9995c2836ab92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560463"
---
# <a name="kspropertyaudioalgorithminstance"></a>KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス


KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス プロパティは、ノードがオーディオ データ ストリームに適用されるサード パーティ製の効果を実現するために使用されるデジタル信号処理 (DSP) アルゴリズムを指定します。 このプロパティに対して定義されている効果には、アコースティック エコー キャンセル機能とノイズの抑制が含まれます。

## <span id="ddk_ksproperty_audio_algorithm_instance_ks"></span><span id="DDK_KSPROPERTY_AUDIO_ALGORITHM_INSTANCE_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、pin がそのデータ ストリームに適用する効果を識別する GUID です。 この値は、ヘッダー ファイル Ksmedia.h から次の Guid のいずれかを指定できます。

<span id="KSALGORITHMINSTANCE_SYSTEM_AGC"></span><span id="ksalgorithminstance_system_agc"></span>KSALGORITHMINSTANCE\_システム\_AGC  
将来使用するために予約されています

<span id="KSALGORITHMINSTANCE_SYSTEM_ACOUSTIC_ECHO_CANCEL"></span><span id="ksalgorithminstance_system_acoustic_echo_cancel"></span>KSALGORITHMINSTANCE\_システム\_音響\_エコー\_キャンセル  
システム既定アコースティック エコー キャンセル アルゴリズム

<span id="KSALGORITHMINSTANCE_SYSTEM_MICROPHONE_ARRAY_PROCESSOR"></span><span id="ksalgorithminstance_system_microphone_array_processor"></span>KSALGORITHMINSTANCE\_システム\_マイク\_配列\_プロセッサ  
将来使用するために予約されています

<span id="KSALGORITHMINSTANCE_SYSTEM_NOISE_SUPPRESS"></span><span id="ksalgorithminstance_system_noise_suppress"></span>KSALGORITHMINSTANCE\_システム\_ノイズ\_を抑制します。  
システム既定のノイズの抑制アルゴリズム

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティを使用して、AEC ノードによって実行される DSP アルゴリズムを制御を ([**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)) ノイズの抑制ノード (または[ **KSNODETYPE\_ノイズ\_抑制**](ksnodetype-noise-suppress.md))。

アルゴリズムのインスタンスの GUID の値に一致する、 **guidDSCFXInstance** 、呼び出し元に渡す DSCEFFECTDESC 構造体のメンバー、 **IDirectSoundCapture::CreateCaptureBuffer**メソッドまたは**DirectSoundFullDuplexCreate**関数。 詳細については、Microsoft Windows SDK のドキュメントを参照してください。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_音響\_エコー\_キャンセル**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_ノイズ\_を抑制します。**](ksnodetype-noise-suppress.md)

 

 







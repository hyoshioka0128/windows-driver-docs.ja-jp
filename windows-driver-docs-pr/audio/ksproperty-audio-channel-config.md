---
title: KSK プロパティ\_AUDIO\_CHANNEL\_構成
description: KSK プロパティ\_AUDIO\_CHANNEL\_CONFIG プロパティは、ノードが出力するオーディオストリーム内のチャネルの実際の空間位置を指定します。
ms.assetid: 5ce9bf4a-c84e-4d7e-8e75-896c88ec1a72
keywords:
- KSPROPERTY_AUDIO_CHANNEL_CONFIG オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHANNEL_CONFIG
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33015cf6c88cedc5f025d281cddc6a498c056232
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831070"
---
# <a name="ksproperty_audio_channel_config"></a>KSK プロパティ\_AUDIO\_CHANNEL\_構成


KSK プロパティ\_AUDIO\_CHANNEL\_CONFIG プロパティは、ノードが出力するオーディオストリーム内のチャネルの実際の空間位置を指定します。

## <span id="ddk_ksproperty_audio_channel_config_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHANNEL_CONFIG_KS"></span>


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
<td align="left"><p>フィルター/ピン留め</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config" data-raw-source="[&lt;strong&gt;KSAUDIO_CHANNEL_CONFIG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)"><strong>KSAUDIO_CHANNEL_CONFIG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、KSAUDIO\_CHANNEL\_CONFIG 型の構造体です。 この構造体は、出力ストリームに含まれるチャネルと、それらのチャネルをスピーカーに割り当てることを指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_CHANNEL\_CONFIG プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DAC ノード ([**KSNODETYPE\_dac**](ksnodetype-dac.md)) または3d ノード ([**KSNODETYPE\_3d\_効果**](ksnodetype-3d-effects.md)) のプロパティとして使用する場合、ksk プロパティ\_AUDIO\_CHANNEL\_CONFIG プロパティで DirectSound スピーカーを指定します。configuration. ステレオスピーカーの構成では、このプロパティを[**Ksk プロパティ\_AUDIO\_ステレオ\_スピーカー\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)プロパティと組み合わせて使用します。これにより、ヘッドホンといくつかのステレオスピーカーが区別されます。構成. スピーカーの構成の詳細については、「 [DirectSound スピーカーの構成設定](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-speaker-configuration-settings)」を参照してください。

また、DirectSound では、KSK プロパティ\_AUDIO\_CHANNEL\_CONFIG プロパティを使用して、チャネル構成の "pan" ノードに対してクエリを実行します。 Pan ノードは、 [DirectSound ノード順序の要件](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-node-ordering-requirements)を満たす、ミキサー pin 上の2番目のボリュームノード ([**KSNODETYPE\_ボリューム**](ksnodetype-volume.md)) です。 **Idirectsoundbuffer:: SetPan**メソッドの DirectSound 実装 (Microsoft Windows SDK ドキュメントで説明) では、pan ノードの[**KSK プロパティ\_AUDIO\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)プロパティを使用して、パンを制御します。

DirectSound では、KSK プロパティ\_AUDIO\_CHANNEL\_CONFIG は、DAC ノードのフィルタープロパティとして、またはボリュームノードと3D ノードのピンプロパティとして扱われます。

また、クライアントはこのプロパティを使用して、 [**KSNODETYPE\_PROLOGIC\_デコーダー**](ksnodetype-prologic-decoder.md)ノードが出力するストリームの形式を選択します。

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

[**KSAUDIO\_チャネル\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)

[**KSNODETYPE\_ボリューム**](ksnodetype-volume.md)

[**KSNODETYPE\_PROLOGIC\_デコーダー**](ksnodetype-prologic-decoder.md)

[**KSK プロパティ\_AUDIO\_ステレオ\_スピーカー\_ジオメトリ**](ksproperty-audio-stereo-speaker-geometry.md)

[**KSK プロパティ\_AUDIO\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

 







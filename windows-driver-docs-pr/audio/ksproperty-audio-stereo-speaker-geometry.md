---
title: KSK プロパティ\_AUDIO\_ステレオ\_スピーカー\_ジオメトリ
description: KSK プロパティ\_AUDIO\_ステレオ\_スピーカー\_GEOMETRY プロパティは、KSK プロパティ\_AUDIO\_CHANNEL\_CONFIG と組み合わせて使用され、の DirectSound スピーカー構成プロパティを実装します。ハードウェアアクセラレータによる3D オーディオ。
ms.assetid: 4a870368-6a9b-41bc-80c3-da6ad1f2454b
keywords:
- KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ddc30c82fe4ede557a1cea6b9c51cf8ac80b2a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830935"
---
# <a name="ksproperty_audio_stereo_speaker_geometry"></a>KSK プロパティ\_AUDIO\_ステレオ\_スピーカー\_ジオメトリ


KSK プロパティ\_AUDIO\_ステレオ\_スピーカー\_GEOMETRY プロパティを[**Ksk プロパティ\_audio\_CHANNEL\_CONFIG**](ksproperty-audio-channel-config.md)と組み合わせて使用して、DirectSound スピーカー構成プロパティを実装します。ハードウェアアクセラレータの3D オーディオの場合。 これは、DAC ノード ([**KSNODETYPE\_dac**](ksnodetype-dac.md)) と3d ノード ([**KSNODETYPE\_3d\_効果**](ksnodetype-3d-effects.md)) のオプションのプロパティです。

## <span id="ddk_ksproperty_audio_stereo_speaker_geometry_ks"></span><span id="DDK_KSPROPERTY_AUDIO_STEREO_SPEAKER_GEOMETRY_KS"></span>


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
<td align="left"><p>ピン/フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は LONG 型で、スピーカーのジオメトリを指定します。 この値は、次のいずれかの定数に設定できます。これは、ヘッダーファイル Ksmedia. h で定義されています。

-   KSK オーディオ\_ステレオ\_スピーカー\_ジオメトリ\_ヘッドホン

-   KSAUDIO\_ステレオ\_スピーカー\_ジオメトリ\_最小

-   KSAUDIO\_ステレオ\_スピーカー\_ジオメトリ\_ナロー

-   KSAUDIO\_ステレオ\_スピーカー\_ジオメトリ\_ワイド

-   KSAUDIO\_ステレオ\_スピーカー\_ジオメトリ\_最大

上記のパラメーターは、 **Idirectsound:: GetSpeakerConfig**メソッド (Microsoft Windows SDK のドキュメントを参照) で使用され、ヘッダーファイル Dsound で定義されている次の値に相当します (値は等しくありません)。

-   DSSPEAKER\_ヘッドフォン

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_最小

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_ナロー

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_ワイド

-   DSSPEAKER\_ステレオ |DSSPEAKER\_GEOMETRY\_最大

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_ステレオ\_スピーカー\_GEOMETRY プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound では、KSK プロパティ\_AUDIO\_ステレオ\_スピーカー\_ジオメトリは、DAC ノードのフィルタープロパティとして、または3D ノードのピンプロパティとして扱われます。

詳細については、「 [DirectSound スピーカー-構成設定](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-speaker-configuration-settings)」を参照してください。

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


[**KSK プロパティ\_AUDIO\_CHANNEL\_構成**](ksproperty-audio-channel-config.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 







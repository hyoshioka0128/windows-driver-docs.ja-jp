---
title: KSK プロパティ\_AUDIO\_QUALITY
description: KSK プロパティ\_AUDIO\_QUALITY プロパティは、ノードの出力ストリームの品質レベルを指定します。 これは、SRC ノード (KSNODETYPE\_SRC) のプロパティです。
ms.assetid: ef57de3b-f7ac-4ecd-915e-27f34fcc2028
keywords:
- KSPROPERTY_AUDIO_QUALITY オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_QUALITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6edce229aee481217e4f443e74ce3be129d1cd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832938"
---
# <a name="ksproperty_audio_quality"></a>KSK プロパティ\_AUDIO\_QUALITY


KSK プロパティ\_AUDIO\_QUALITY プロパティは、ノードの出力ストリームの品質レベルを指定します。 これは、SRC ノード ([**KSNODETYPE\_src**](ksnodetype-src.md)) のプロパティです。

## <span id="ddk_ksproperty_audio_quality_ks"></span><span id="DDK_KSPROPERTY_AUDIO_QUALITY_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は ULONG 型で、出力ストリームの品質レベルを示します。 この値は、ヘッダーファイル Ksmedia. h の次のいずれかの定数に設定する必要があります。

<span id="KSAUDIO_QUALITY_WORST"></span><span id="ksaudio_quality_worst"></span>KSAUDIO\_品質\_最悪  
最低品質

<span id="KSAUDIO_QUALITY_PC"></span><span id="ksaudio_quality_pc"></span>KSAUDIO\_QUALITY\_PC  
Standard コンピューターの品質 (制約なし)

<span id="KSAUDIO_QUALITY_BASIC"></span><span id="ksaudio_quality_basic"></span>KSAUDIO\_QUALITY\_BASIC  
基本 (低-エンド) コンシューマーオーディオ品質 (既定値)

<span id="KSAUDIO_QUALITY_ADVANCED"></span><span id="ksaudio_quality_advanced"></span>KSK オーディオ\_品質\_詳細設定  
高度な (ハイエンド) コンシューマーオーディオ品質

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_QUALITY プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

[KMixer システムドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components#kmixer-system-driver)によって実行されるサンプル速度変換の種類の詳細については、「 [KMixer Driver sample Rate Conversion and 混合ポリシー](https://docs.microsoft.com/windows-hardware/drivers/audio/kmixer-driver-sample-rate-conversion-and-mixing-policy)」を参照してください。

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


[**KSNODETYPE\_SRC**](ksnodetype-src.md)

[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

 

 







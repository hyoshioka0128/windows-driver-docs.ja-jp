---
title: KSK プロパティ\_AUDIO\_動的\_サンプリング\_率
description: KSK プロパティ\_AUDIO\_DYNAMIC\_サンプリング\_RATE プロパティは、ノードのサンプリングレートの動的追跡を有効または無効にするために使用されます。
ms.assetid: ff99c670-ef93-4730-8be4-1ed7c01c5381
keywords:
- KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d66697fc24017149bf2d6553047a6160d0adc82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833044"
---
# <a name="ksproperty_audio_dynamic_sampling_rate"></a>KSK プロパティ\_AUDIO\_動的\_サンプリング\_率


KSK プロパティ\_AUDIO\_DYNAMIC\_サンプリング\_RATE プロパティは、ノードのサンプリングレートの動的追跡を有効または無効にするために使用されます。

## <span id="ddk_ksproperty_audio_dynamic_sampling_rate_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE_KS"></span>


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
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール型で、ノードで動的追跡を有効にするか無効にするかを指定します。 サンプリングレートの動的追跡が有効になっている場合、値は**TRUE**になります。 このモードでは、入力ストリームのサンプリングレートを明示的に変化させることができます。これを行うには、入力ストリームのタイムスタンプを設定して、 [**Ksk プロパティ\_AUDIO\_サンプリング\_レート**](ksproperty-audio-sampling-rate.md)を設定するか、暗黙的に設定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_DYNAMIC\_サンプリング\_RATE プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、次のノードの種類で動的追跡を制御するために使用されます。

-   ADC ノード ([**KSNODETYPE\_adc**](ksnodetype-adc.md))

-   DAC ノード ([**KSNODETYPE\_dac**](ksnodetype-dac.md))

-   SRC ノード ([**KSNODETYPE\_src**](ksnodetype-src.md))

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

[**KSK プロパティ\_AUDIO\_サンプリング\_率**](ksproperty-audio-sampling-rate.md)

[**KSNODETYPE\_ADC**](ksnodetype-adc.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_SRC**](ksnodetype-src.md)

 

 







---
title: KSPROPERTY\_オーディオ\_動的\_サンプリング\_率
description: KSPROPERTY\_オーディオ\_動的\_サンプリング\_レートのプロパティを使用して有効にして、ノードのサンプリング レートの動的な追跡を無効にします。
ms.assetid: ff99c670-ef93-4730-8be4-1ed7c01c5381
keywords:
- KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE オーディオ デバイス
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
ms.openlocfilehash: 8b2d397cf438d31988b4fe0424ab313f891bf2fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358935"
---
# <a name="kspropertyaudiodynamicsamplingrate"></a>KSPROPERTY\_オーディオ\_動的\_サンプリング\_率


KSPROPERTY\_オーディオ\_動的\_サンプリング\_レートのプロパティを使用して有効にして、ノードのサンプリング レートの動的な追跡を無効にします。

## <span id="ddk_ksproperty_audio_dynamic_sampling_rate_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DYNAMIC_SAMPLING_RATE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は BOOL 型で、動的の追跡が有効になっているまたはノードで無効になっているかどうかを指定します。 値が**TRUE**サンプリング レートの動的な追跡が有効になっています。 このモードで、入力ストリームのサンプリング レート変更するには明示的に使用率を設定して[ **KSPROPERTY\_オーディオ\_サンプリング\_レート**](ksproperty-audio-sampling-rate.md)または入力ストリームにタイムスタンプをレートを設定によって暗黙的にします。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_動的\_サンプリング\_レート プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、コントロールで次のノード タイプの追跡を動的に使用されます。

-   ADC ノード ([**KSNODETYPE\_ADC**](ksnodetype-adc.md))

-   DAC のノード ([**KSNODETYPE\_DAC**](ksnodetype-dac.md))

-   SRC ノード ([**KSNODETYPE\_SRC**](ksnodetype-src.md))

<a name="requirements"></a>必要条件
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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSPROPERTY\_オーディオ\_サンプリング\_率**](ksproperty-audio-sampling-rate.md)

[**KSNODETYPE\_ADC**](ksnodetype-adc.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_SRC**](ksnodetype-src.md)

 

 







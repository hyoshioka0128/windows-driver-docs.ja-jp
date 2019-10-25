---
title: KSK プロパティ\_オーディオ\_低音\_ブースト
description: KSK プロパティ\_AUDIO\_低音\_ブーストプロパティを使用すると、トーンノード (KSNODETYPE\_声調) でのチャネルの低音ブーストが有効になり、無効になります。
ms.assetid: aa54b88b-e251-4d16-9ced-842fec569914
keywords:
- KSPROPERTY_AUDIO_BASS_BOOST オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_BASS_BOOST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925cdbb2481eb6c4366b5a942ba671f6686f47f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833047"
---
# <a name="ksproperty_audio_bass_boost"></a>KSK プロパティ\_オーディオ\_低音\_ブースト


KSK プロパティ\_AUDIO\_低音\_ブーストプロパティを使用すると、トーンノード ([**KSNODETYPE\_声調**](ksnodetype-tone.md)) でのチャネルの低音ブーストが有効になり、無効になります。

## <span id="ddk_ksproperty_audio_bass_boost_ks"></span><span id="DDK_KSPROPERTY_AUDIO_BASS_BOOST_KS"></span>


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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) はブール型で、低音ブーストがオンまたはオフになっているかどうかを示します。 値が**TRUE**の場合は、指定されたチャネルに対して低音ブーストがオンになっていることを示します。 **FALSE**は、無効であることを示します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_低音\_ブーストプロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

トーンノードでは、高音レベル、ミッド周波数レベル、低音レベル、低音ブーストを制御するプロパティをサポートできます。 詳細については、「 [**KSNODETYPE\_声調**](ksnodetype-tone.md)」を参照してください。

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


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE\_声調**](ksnodetype-tone.md)

 

 







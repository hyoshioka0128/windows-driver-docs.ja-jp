---
title: KSK プロパティ\_AUDIO\_MID
description: KSK プロパティ\_AUDIO\_MID プロパティは、トーンノード (KSNODETYPE\_声調) でのチャネルの中間周波数レベルを指定します。
ms.assetid: cb2555d4-5224-42a6-b364-70de91a44924
keywords:
- KSPROPERTY_AUDIO_MID オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ced9889c6fd82adbc76310f4820e13407550bd6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832979"
---
# <a name="ksproperty_audio_mid"></a>KSK プロパティ\_AUDIO\_MID


KSK プロパティ\_AUDIO\_MID プロパティは、トーンノード ([**KSNODETYPE\_声調**](ksnodetype-tone.md)) でのチャネルの中間周波数レベルを指定します。

## <span id="ddk_ksproperty_audio_mid_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MID_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は LONG 型で、mid frequency レベルを指定します。 レベル値には次のスケールが使用されます。

-2147483648 は-無限大デシベル (減衰),

-2147483647 は-32767.99998474 デシベル (減衰)、および

\+ 2147483647 は + 32767.99998474 デシベル (ゲイン) です。

2147483648 ~ + 2147483647 の整数値で表されるデシベル範囲。ここで、

このスケールの解像度は1/65536 デシベルです。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_MID プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

フィルターは、KSK プロパティ\_AUDIO\_MID プロパティに成功します。このプロパティは、フィルターの範囲を超える値を指定しますが、値はサポートされている範囲にクランプされます。 ただし、このプロパティを取得するための後続の要求では、使用される実際の値が出力されます。

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

 

 







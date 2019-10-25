---
title: KSK プロパティ\_AC3\_ビット\_ストリーム\_モード
description: KSK プロパティ\_AC3\_BIT\_STREAM\_MODE プロパティは、AC-3 ストリームにエンコードされるオーディオサービスの種類であるビットストリームモードを指定します。
ms.assetid: ee3705f5-f16d-4f5e-a551-bea8986d88b6
keywords:
- KSPROPERTY_AC3_BIT_STREAM_MODE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_BIT_STREAM_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a6d4e1d1247c8c9bf58a22810b16637fdab6c1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831143"
---
# <a name="ksproperty_ac3_bit_stream_mode"></a>KSK プロパティ\_AC3\_ビット\_ストリーム\_モード


KSK プロパティ\_AC3\_BIT\_STREAM\_MODE プロパティは、AC-3 ストリームにエンコードされるオーディオサービスの種類であるビットストリームモードを指定します。

## <span id="ddk_ksproperty_ac3_bit_stream_mode_ks"></span><span id="DDK_KSPROPERTY_AC3_BIT_STREAM_MODE_KS"></span>


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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_bit_stream_mode" data-raw-source="[&lt;strong&gt;KSAC3_BIT_STREAM_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_bit_stream_mode)"><strong>KSAC3_BIT_STREAM_MODE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ビットストリームモードを指定する KSAC3\_ビット\_ストリーム\_モード構造体です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AC3\_ビット\_ストリーム\_モードプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAC3\_ビット\_ストリーム\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_bit_stream_mode)

 

 







---
title: KSK プロパティ\_AC3\_部屋\_種類
description: KSK プロパティ\_AC3\_ROOM\_TYPE プロパティは、最終的なオーディオセッションが生成されたミックスルームの種類と調整を指定します。
ms.assetid: 4e160fda-01f2-4517-bbc3-a9ae5b19f6c2
keywords:
- KSPROPERTY_AC3_ROOM_TYPE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_ROOM_TYPE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff409c0bb2aa0adf8d24696ab87e74e794096a0d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831164"
---
# <a name="ksproperty_ac3_room_type"></a>KSK プロパティ\_AC3\_部屋\_種類


KSK プロパティ\_AC3\_ROOM\_TYPE プロパティは、最終的なオーディオセッションが生成されたミックスルームの種類と調整を指定します。

## <span id="ddk_ksproperty_ac3_room_type_ks"></span><span id="DDK_KSPROPERTY_AC3_ROOM_TYPE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_room_type" data-raw-source="[&lt;strong&gt;KSAC3_ROOM_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_room_type)"><strong>KSAC3_ROOM_TYPE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、KSAC3\_ルーム\_型の構造体で、AC 3 エンコードストリームが生成されたミックスルームの種類を指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AC3\_ROOM\_TYPE プロパティ要求は正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、AC 3 でエンコードされたストリームの運用環境に関する情報を提供します。 プロパティ値は通常、AC 3 デコーダーでは使用されませんが、他のオーディオコンポーネントで使用される可能性があります。

エンコードされたストリームが部屋の種類を指定しない場合、プロパティ要求はエラーコードを返します。

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

[**KSAC3\_ルーム\_種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_room_type)

 

 







---
title: KSPROPERTY\_AC3\_ルーム\_型
description: KSPROPERTY\_AC3\_ルーム\_TYPE プロパティは、型と最終的な音声セッションが生成された混合部屋の調整を指定します。
ms.assetid: 4e160fda-01f2-4517-bbc3-a9ae5b19f6c2
keywords:
- KSPROPERTY_AC3_ROOM_TYPE オーディオ デバイス
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
ms.openlocfilehash: e1a765e026b7c4a7c14b04b1e41b376f1d1a69d3
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391488"
---
# <a name="kspropertyac3roomtype"></a>KSPROPERTY\_AC3\_ルーム\_型


KSPROPERTY\_AC3\_ルーム\_TYPE プロパティは、型と最終的な音声セッションが生成された混合部屋の調整を指定します。

## <span id="ddk_ksproperty_ac3_room_type_ks"></span><span id="DDK_KSPROPERTY_AC3_ROOM_TYPE_KS"></span>


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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_room_type" data-raw-source="[&lt;strong&gt;KSAC3_ROOM_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_room_type)"><strong>KSAC3_ROOM_TYPE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSAC3\_ルーム\_AC で 3 でエンコードされたストリームが生成された部屋の混在の種類を指定する型の構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AC3\_ルーム\_プロパティ要求の種類のステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、AC で 3 でエンコードされたストリームの運用環境に関する情報を提供します。 プロパティの値は、ac-3 デコーダーで通常使用されていないが、その他のオーディオのコンポーネントで使用する場合があります。

エンコードされたストリームが部屋の種類を指定しない場合、プロパティの要求には、エラー コードが返されます。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSAC3\_ROOM\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksac3_room_type)

 

 







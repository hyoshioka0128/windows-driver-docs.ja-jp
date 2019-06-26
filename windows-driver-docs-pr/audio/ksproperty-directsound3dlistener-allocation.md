---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_割り当て
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_割り当てのプロパティを使用して割り当て、そのリスナーのデータのストレージを解放する場合、ドライバーに指示します。
ms.assetid: 2e7256d0-578d-4b6e-aa5f-9e42e649523b
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79da77eda810cb0a972b1512b2569c2bc0ea9933
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361030"
---
# <a name="kspropertydirectsound3dlistenerallocation"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_割り当て


KSPROPERTY\_DIRECTSOUND3DLISTENER\_割り当てのプロパティを使用して割り当て、そのリスナーのデータのストレージを解放する場合、ドライバーに指示します。 リスナーが作成され、リスナーが削除されたときに解放されるときに、ストレージが割り当てられます。 このプロパティは、クエリでは、リスナーのデータが現在割り当てられているかどうかをドライバーにも使用できます。

## <span id="ddk_ksproperty_directsound3dlistener_allocation_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、BOOL 型のです。 プロパティの設定要求の場合は、この値は、ドライバーの割り当てする必要がありますやそのリスナーのデータのストレージを解放するかどうかを指定します。

-   値**TRUE**そのリスナーのデータのストレージを割り当てるために、ドライバーに指示します。

-   値**FALSE**リスナー データを解放するドライバーに指示します。

プロパティの get 要求の値の**TRUE**または**FALSE**ドライバーが現在のリスナーのデータ記憶域の割り当てを保持しているかどうかを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DLISTENER\_プロパティの割り当て要求のステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

 

 







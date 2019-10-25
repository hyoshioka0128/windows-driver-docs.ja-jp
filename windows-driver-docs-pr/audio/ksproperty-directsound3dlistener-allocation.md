---
title: KSK プロパティ\_DIRECTSOUND3DLISTENER\_ALLOCATION
description: KSK プロパティ\_DIRECTSOUND3DLISTENER\_ALLOCATION プロパティを使用して、リスナーデータ用の記憶域を割り当てて解放するタイミングをドライバーに指示します。
ms.assetid: 2e7256d0-578d-4b6e-aa5f-9e42e649523b
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION オーディオデバイス
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
ms.openlocfilehash: 9c8ae38b3fbe43e704b117ff9c891fa6bc7ce923
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832819"
---
# <a name="ksproperty_directsound3dlistener_allocation"></a>KSK プロパティ\_DIRECTSOUND3DLISTENER\_ALLOCATION


KSK プロパティ\_DIRECTSOUND3DLISTENER\_ALLOCATION プロパティを使用して、リスナーデータ用の記憶域を割り当てて解放するタイミングをドライバーに指示します。 ストレージは、リスナーの作成時に割り当てられ、リスナーが削除されると解放されます。 このプロパティは、リスナーデータが現在割り当てられているかどうかをドライバーに照会するためにも使用できます。

## <span id="ddk_ksproperty_directsound3dlistener_allocation_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は BOOL です。 プロパティの設定要求では、この値によって、ドライバーがリスナーデータ用の記憶域を割り当てるか、または解放する必要があるかを指定します。

-   値が**TRUE**の場合、ドライバーはリスナーデータ用に記憶域を割り当てるように指示します。

-   値が**FALSE**の場合は、リスナーデータを解放するようにドライバーに指示します。

Get property 要求の場合、値が**TRUE**または**FALSE**の場合は、ドライバーがリスナーデータのストレージ割り当てを現在保持しているかどうかを示します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DLISTENER\_ALLOCATION property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

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

 

 







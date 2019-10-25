---
title: KSPROPERTY\_AC3\_エラー\_CONCEALMENT
description: KSK プロパティ\_AC3\_ERROR\_CONCEALMENT プロパティは、再生中に AC 3 エンコードストリームのエラーを非隠れにする方法を指定します。
ms.assetid: bdf3dd8f-0757-4679-b051-63736503c5b4
keywords:
- KSPROPERTY_AC3_ERROR_CONCEALMENT オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_ERROR_CONCEALMENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08733b89c5795cf29e8ec2130799c00f6a1bc3b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831139"
---
# <a name="ksproperty_ac3_error_concealment"></a>KSPROPERTY\_AC3\_エラー\_CONCEALMENT


KSK プロパティ\_AC3\_ERROR\_CONCEALMENT プロパティは、再生中に AC 3 エンコードストリームのエラーを非隠れにする方法を指定します。

## <span id="ddk_ksproperty_ac3_error_concealment_ks"></span><span id="DDK_KSPROPERTY_AC3_ERROR_CONCEALMENT_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment" data-raw-source="[&lt;strong&gt;KSAC3_ERROR_CONCEALMENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment)"><strong>KSAC3_ERROR_CONCEALMENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、KSAC3\_ERROR\_CONCEALMENT 構造体で、エラーを含む AC 3 ブロックをどのように隠しておくかを指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

\_AC3\_エラー\_CONCEALMENT property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

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

[**KSAC3\_エラー\_CONCEALMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksac3_error_concealment)

 

 







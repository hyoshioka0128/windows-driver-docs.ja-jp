---
title: KSK プロパティ\_HRTF3D\_フィルター\_形式
description: KSK プロパティ\_HRTF3D\_FILTER\_FORMAT プロパティは、HRTF アルゴリズムで使用されるフィルター形式を取得します。
ms.assetid: 7e4e869e-60ae-4266-93e4-0b6118951417
keywords:
- KSPROPERTY_HRTF3D_FILTER_FORMAT オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_HRTF3D_FILTER_FORMAT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df2107db2b2940ae8dc265d9de5d017d87a9422e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830708"
---
# <a name="ksproperty_hrtf3d_filter_format"></a>KSK プロパティ\_HRTF3D\_フィルター\_形式


KSK プロパティ\_HRTF3D\_FILTER\_FORMAT プロパティは、HRTF アルゴリズムで使用されるフィルター形式を取得します。

## <span id="ddk_ksproperty_hrtf3d_filter_format_ks"></span><span id="DDK_KSPROPERTY_HRTF3D_FILTER_FORMAT_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg" data-raw-source="[&lt;strong&gt;KSDS3D_HRTF_FILTER_FORMAT_MSG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)"><strong>KSDS3D_HRTF_FILTER_FORMAT_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、HRTF アルゴリズムのフィルターメソッドと係数の形式を指定する KSDS3D\_HRTF\_FILTER\_形式\_MSG の構造体です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_HRTF3D\_FILTER\_FORMAT プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

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

[**KSDS3D\_HRTF\_FILTER\_FORMAT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)

 

 







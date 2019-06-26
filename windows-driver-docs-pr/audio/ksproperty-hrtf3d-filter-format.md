---
title: KSPROPERTY\_HRTF3D\_フィルター\_形式
description: KSPROPERTY\_HRTF3D\_フィルター\_FORMAT プロパティ HRTF アルゴリズムで使用されるフィルターの形式を取得します。
ms.assetid: 7e4e869e-60ae-4266-93e4-0b6118951417
keywords:
- KSPROPERTY_HRTF3D_FILTER_FORMAT オーディオ デバイス
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
ms.openlocfilehash: 10f6c812e1f85066120b7bca0b35f8ff97acd6ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358787"
---
# <a name="kspropertyhrtf3dfilterformat"></a>KSPROPERTY\_HRTF3D\_フィルター\_形式


KSPROPERTY\_HRTF3D\_フィルター\_FORMAT プロパティ HRTF アルゴリズムで使用されるフィルターの形式を取得します。

## <span id="ddk_ksproperty_hrtf3d_filter_format_ks"></span><span id="DDK_KSPROPERTY_HRTF3D_FILTER_FORMAT_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg" data-raw-source="[&lt;strong&gt;KSDS3D_HRTF_FILTER_FORMAT_MSG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)"><strong>KSDS3D_HRTF_FILTER_FORMAT_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSDS3D の構造体\_HRTF\_フィルター\_形式\_HRTF アルゴリズムのフィルターのメソッドと係数の形式を指定するメッセージ。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_HRTF3D\_フィルター\_書式設定プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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

[**KSDS3D\_HRTF\_FILTER\_FORMAT\_MSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)

 

 







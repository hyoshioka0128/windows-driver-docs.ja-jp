---
title: KSPROPERTY\_HRTF3D\_初期化
description: KSPROPERTY\_HRTF3D\_初期化プロパティを HRTF アルゴリズムを初期化するために使用するパラメーター値を指定します。
ms.assetid: 45c6c80a-caea-4fb2-a8c8-f64130c0f837
keywords:
- KSPROPERTY_HRTF3D_INITIALIZE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_HRTF3D_INITIALIZE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04f2ef446f34e1d1b3db371dad704fc4f1663203
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532062"
---
# <a name="kspropertyhrtf3dinitialize"></a>KSPROPERTY\_HRTF3D\_初期化


KSPROPERTY\_HRTF3D\_初期化プロパティを HRTF アルゴリズムを初期化するために使用するパラメーター値を指定します。

## <span id="ddk_ksproperty_hrtf3d_initialize_ks"></span><span id="DDK_KSPROPERTY_HRTF3D_INITIALIZE_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537106" data-raw-source="[&lt;strong&gt;KSDS3D_HRTF_INIT_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537106)"><strong>KSDS3D_HRTF_INIT_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSDS3D の構造体\_HRTF\_INIT\_MSG 初期化値を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_HRTF3D\_初期化プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSDS3D\_HRTF\_INIT\_メッセージ**](https://msdn.microsoft.com/library/windows/hardware/ff537106)

 

 







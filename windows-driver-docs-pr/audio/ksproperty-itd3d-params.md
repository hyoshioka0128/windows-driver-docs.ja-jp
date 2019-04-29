---
title: KSPROPERTY\_ITD3D\_PARAMS
description: KSPROPERTY\_ITD3D\_PARAMS プロパティを使用して、3 D のノードの ITD アルゴリズムによって使用されるパラメーターを設定します。
ms.assetid: c6f87087-3c91-46a4-b40e-078d0a015c4c
keywords:
- KSPROPERTY_ITD3D_PARAMS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ITD3D_PARAMS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e540171f29ca3fce9ef873d6945825362c0d75b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332701"
---
# <a name="kspropertyitd3dparams"></a>KSPROPERTY\_ITD3D\_PARAMS


KSPROPERTY\_ITD3D\_PARAMS プロパティを使用して、3 D のノードの ITD アルゴリズムによって使用されるパラメーターを設定します。

## <span id="ddk_ksproperty_itd3d_params_ks"></span><span id="DDK_KSPROPERTY_ITD3D_PARAMS_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537114" data-raw-source="[&lt;strong&gt;KSDS3D_ITD_PARAMS_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537114)"><strong>KSDS3D_ITD_PARAMS_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSDS3D の構造体\_ITD\_PARAMS\_ITD アルゴリズムのパラメーターを指定するメッセージ。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_ITD3D\_PARAMS プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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

[**KSDS3D\_ITD\_PARAMS\_メッセージ**](https://msdn.microsoft.com/library/windows/hardware/ff537114)

 

 







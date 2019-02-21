---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES プロパティは、内側と 3D のサウンド バッファーのプロジェクションのサウンド コーンの外側の円錐の角度を指定します。
ms.assetid: a3978aaf-218c-4021-abf0-e426eacf52c7
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d38ac250b0408128ab139e29a6f88418fe6a75a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539157"
---
# <a name="kspropertydirectsound3dbufferconeangles"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES


KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES プロパティは、内側と 3D のサウンド バッファーのプロジェクションのサウンド コーンの外側の円錐の角度を指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_coneangles_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES_KS"></span>


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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537103" data-raw-source="[&lt;strong&gt;KSDS3D_BUFFER_CONE_ANGLES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537103)"><strong>KSDS3D_BUFFER_CONE_ANGLES</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSDS3D の構造体\_バッファー\_CONE\_内側と外側の円錐の角度を指定する角度。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

内側と外側の円錐の角度 DirectSound 3D バッファーのプロジェクションのサウンド コーンの詳細については、Microsoft Windows SDK のドキュメントでは、次を参照してください。

-   **DwInsideConeAngle**と**dwOutsideConeAngle** DS3DBUFFER 構造体のメンバー。

-   **IDirectSound3DBuffer::GetConeAngles**と**IDirectSound3DBuffer::SetConeAngles**メソッド。

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

[**KSDS3D\_バッファー\_CONE\_角度**](https://msdn.microsoft.com/library/windows/hardware/ff537103)

 

 







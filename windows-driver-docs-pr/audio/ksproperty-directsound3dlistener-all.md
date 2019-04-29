---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_すべて
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_すべてのプロパティを使用して、指定されたリスナー id DirectSound 3D リスナーのすべてのプロパティを取得または設定
ms.assetid: cdf98ed6-cd8e-480c-b766-c348f41919ef
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64b067aca3265c18f1dec8a692a449f6c92cc077
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332802"
---
# <a name="kspropertydirectsound3dlistenerall"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_すべて


KSPROPERTY\_DIRECTSOUND3DLISTENER\_すべてのプロパティを使用して、指定されたリスナー id DirectSound 3D リスナーのすべてのプロパティを取得または設定

## <span id="ddk_ksproperty_directsound3dlistener_all_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ALL_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537116" data-raw-source="[&lt;strong&gt;KSDS3D_LISTENER_ALL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537116)"><strong>KSDS3D_LISTENER_ALL</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSDS3D の構造体\_リスナー\_すべて 3D リスナーのすべてのプロパティを指定します。 この構造体は、Microsoft Windows SDK ドキュメントに記載されている DS3DBUFFER 構造に似ています。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DLISTENER\_プロパティのすべての要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound は、このプロパティを使用して、実装する、 **IDirectSound3DBuffer::GetAllParameters**と**IDirectSound3DBuffer::SetAllParameters**メソッドで、Windows SDK に記載されていますドキュメントです。

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

[**KSDS3D\_リスナー\_すべて**](https://msdn.microsoft.com/library/windows/hardware/ff537116)

 

 







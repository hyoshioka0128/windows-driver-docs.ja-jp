---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR プロパティは、3 D リスナーのロールオフ係数を指定します。
ms.assetid: 3eef80ef-921b-4364-b31d-14a62f305f5d
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d47d713396e214fa96080b898d600a4bd295f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560744"
---
# <a name="kspropertydirectsound3dlistenerrollofffactor"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR


KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR プロパティは、3 D リスナーのロールオフ係数を指定します。

## <span id="ddk_ksproperty_directsound3dlistener_rollofffactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR_KS"></span>


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
<td align="left"><p>FLOAT</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は FLOAT 型のロールオフ係数を指定します。 ロールオフ係数の範囲は DS3D\_DS3D に MINROLLOFFFACTOR\_MAXROLLOFFFACTOR で、それぞれ 0.0 と 10.0 として定義されます。 既定のロールオフ係数は DS3D\_DEFAULTROLLOFFFACTOR、1.0 として定義されています。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

ロールオフでは、減衰サウンドのソースからのリスナーの距離に基づいて、サウンドに適用されるを指定します。 0 のロールオフ係数を減衰には適用されません、サウンドの距離に関係なく、リスナーからを意味します。 1 より大きい要因が誇張実際減衰サウンドの距離の。

DirectSound は、このプロパティを使用して、実装する、 **IDirectSound3DListener::GetRolloffFactor**と**IDirectSound3DListener::SetRolloffFactor**メソッドで、Microsoft に記載されていますWindows SDK のドキュメントです。

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

 

 







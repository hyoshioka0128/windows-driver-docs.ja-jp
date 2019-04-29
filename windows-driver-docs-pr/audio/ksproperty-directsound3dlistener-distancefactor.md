---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR プロパティは、距離の値に適用されるまでの距離係数を指定します。
ms.assetid: 38daa5d8-d70f-4484-bf5a-a9a365296313
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48168c1710bda956ff7c6f746a0cb600a3dff327
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332754"
---
# <a name="kspropertydirectsound3dlistenerdistancefactor"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR


KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR プロパティは、距離の値に適用されるまでの距離係数を指定します。

## <span id="ddk_ksproperty_directsound3dlistener_distancefactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR_KS"></span>


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

 

プロパティ値 (データの操作) は FLOAT 型の距離の係数を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

KSPROPSETID の距離\_DirectSound3DBuffer と KSPROPSETID\_DirectSound3DListener プロパティは、メーター距離係数時間の単位で表されます。

既定では、距離の係数は 1、メートル単位で距離の単位はそのためです。 (また、ベロシティの既定の単位は 1 秒あたりのメートル数) です。

クライアントの距離単位を変更することができます、 **KSPROPSETID\_DirectSound3DBuffer**と**KSPROPSETID\_DirectSound3DListener** KSPROPERTYを送信することによってプロパティ\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR プロパティの設定要求さまざまな distance 係数を指定します。

DirectSound は、このプロパティを使用して、実装する、 **IDirectSound3DListener::GetDistanceFactor**と**IDirectSound3DListener::SetDistanceFactor**メソッドで、Microsoft に記載されていますWindows SDK のドキュメントです。

<a name="requirements"></a>必要条件
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

 

 







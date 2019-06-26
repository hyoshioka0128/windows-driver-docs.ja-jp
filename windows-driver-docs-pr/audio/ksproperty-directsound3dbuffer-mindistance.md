---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE プロパティが 3D サウンド バッファーの最小距離を指定します。
ms.assetid: 998e591d-7c23-4857-908c-4e90918c9a94
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fe5a550bdea609cfd1b14fbf1b28875cc2026c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358804"
---
# <a name="kspropertydirectsound3dbuffermindistance"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE


KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE プロパティが 3D サウンド バッファーの最小距離を指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_mindistance_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>FLOAT</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は FLOAT 型の最小の距離を指定します。 距離単位については、次を参照してください。 [ **KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DBUFFER\_MINDISTANCE プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

距離を最短距離をサウンドの元よりも小さいか、サウンドのボリュームされなくにつれて、距離は小さくなります。 DirectSound 3D バッファーの最小距離の詳細については、Microsoft Windows SDK のドキュメントでは、次を参照してください。

-   **FlMinDistance** DS3DBUFFER 構造体のメンバー。

-   **IDirectSound3DBuffer::GetMinDistance**と**IDirectSound3DBuffer::SetMinDistance**メソッド。

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

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

 

 







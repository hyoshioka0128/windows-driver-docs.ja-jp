---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_すべて
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_を取得または指定したバッファーの DirectSound 3D バッファーのすべてのプロパティを設定するすべてのプロパティを使用します。
ms.assetid: 7c62a0f2-080b-42cd-a30e-7ceb5edad894
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_ALL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_ALL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2181ad95462acf46b91f4b4bfbbcff1392057797
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360558"
---
# <a name="kspropertydirectsound3dbufferall"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_すべて


KSPROPERTY\_DIRECTSOUND3DBUFFER\_を取得または指定したバッファーの DirectSound 3D バッファーのすべてのプロパティを設定するすべてのプロパティを使用します。

## <span id="ddk_ksproperty_directsound3dbuffer_all_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_ALL_KS"></span>


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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_buffer_all" data-raw-source="[&lt;strong&gt;KSDS3D_BUFFER_ALL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_buffer_all)"><strong>KSDS3D_BUFFER_ALL</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSDS3D の構造体\_バッファー\_すべてバッファーの 3D の特性を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_DIRECTSOUND3DBUFFER\_プロパティのすべての要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

KSDS3D\_バッファー\_すべての構造は、Microsoft Windows SDK ドキュメントで説明されている DS3DBUFFER 構造と似ています。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSDS3D\_バッファー\_すべて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_buffer_all)

 

 







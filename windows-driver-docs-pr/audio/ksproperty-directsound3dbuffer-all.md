---
title: KSK プロパティ\_DIRECTSOUND3DBUFFER\_すべて
description: 指定したバッファーのすべての DirectSound 3D バッファープロパティを取得または設定するには、KSK プロパティ\_DIRECTSOUND3DBUFFER\_ALL プロパティを使用します。
ms.assetid: 7c62a0f2-080b-42cd-a30e-7ceb5edad894
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_ALL オーディオデバイス
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
ms.openlocfilehash: 8b3bcdd64cf812158e58ea6d023e9cf1cc0edf2f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830842"
---
# <a name="ksproperty_directsound3dbuffer_all"></a>KSK プロパティ\_DIRECTSOUND3DBUFFER\_すべて


指定したバッファーのすべての DirectSound 3D バッファープロパティを取得または設定するには、KSK プロパティ\_DIRECTSOUND3DBUFFER\_ALL プロパティを使用します。

## <span id="ddk_ksproperty_directsound3dbuffer_all_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_ALL_KS"></span>


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
<td align="left"><p>[はい]</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all" data-raw-source="[&lt;strong&gt;KSDS3D_BUFFER_ALL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all)"><strong>KSDS3D_BUFFER_ALL</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、KSDS3D\_\_BUFFER 型の構造体で、バッファーの3D 特性を指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DBUFFER\_すべてのプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

すべての構造\_KSDS3D\_BUFFER は、Microsoft Windows SDK のドキュメントで説明されている DS3DBUFFER 構造体に似ています。

DirectSound は、このプロパティを使用して**IDirectSound3DBuffer:: GetAllParameters**メソッドと**IDirectSound3DBuffer:: setallparameters**メソッドを実装します。これについては、Windows SDK のドキュメントを参照してください。

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

[**KSDS3D\_バッファー\_すべて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all)

 

 







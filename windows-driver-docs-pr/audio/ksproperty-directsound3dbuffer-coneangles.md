---
title: KSK プロパティ\_DIRECTSOUND3DBUFFER\_CONEANGLES
description: KSK プロパティ\_DIRECTSOUND3DBUFFER\_CONEANGLES プロパティは、3D サウンドバッファーのサウンドプロジェクションコーンの内部および外部のコーンの角度を指定します。
ms.assetid: a3978aaf-218c-4021-abf0-e426eacf52c7
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES オーディオデバイス
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
ms.openlocfilehash: fc8a90a0cf85323d1f3c1d28dacb8b5847157b0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832835"
---
# <a name="ksproperty_directsound3dbuffer_coneangles"></a>KSK プロパティ\_DIRECTSOUND3DBUFFER\_CONEANGLES


KSK プロパティ\_DIRECTSOUND3DBUFFER\_CONEANGLES プロパティは、3D サウンドバッファーのサウンドプロジェクションコーンの内部および外部のコーンの角度を指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_coneangles_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles" data-raw-source="[&lt;strong&gt;KSDS3D_BUFFER_CONE_ANGLES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles)"><strong>KSDS3D_BUFFER_CONE_ANGLES</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、KSDS3D\_BUFFER 型の構造体であり、円錐の内側と外側の角度を指定する円錐\_角度\_ます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DBUFFER\_CONEANGLES プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound 3D バッファーのサウンドプロジェクションコーンの内部および外部のコーン角度の詳細については、Microsoft Windows SDK のドキュメントで次を参照してください。

-   DS3DBUFFER 構造体の**Dwinsideconeangle**メンバーと**dwOutsideConeAngle**メンバー。

-   **IDirectSound3DBuffer:: getconeangles**と**IDirectSound3DBuffer:: setconeangles**メソッド。

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

[**KSDS3D\_バッファー\_円錐\_角度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles)

 

 







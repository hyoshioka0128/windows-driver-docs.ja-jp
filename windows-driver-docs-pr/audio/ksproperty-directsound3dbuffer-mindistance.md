---
title: KSK プロパティ\_DIRECTSOUND3DBUFFER\_MINDISTANCE
description: KSK プロパティ\_DIRECTSOUND3DBUFFER\_MINDISTANCE プロパティは、3D サウンドバッファーの最小距離を指定します。
ms.assetid: 998e591d-7c23-4857-908c-4e90918c9a94
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE オーディオデバイス
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
ms.openlocfilehash: d2786d50a84b31f4964cdf8be8753d8deb774a12
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830825"
---
# <a name="ksproperty_directsound3dbuffer_mindistance"></a>KSK プロパティ\_DIRECTSOUND3DBUFFER\_MINDISTANCE


KSK プロパティ\_DIRECTSOUND3DBUFFER\_MINDISTANCE プロパティは、3D サウンドバッファーの最小距離を指定します。

## <span id="ddk_ksproperty_directsound3dbuffer_mindistance_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>FLOAT</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は FLOAT 型で、最小距離を指定します。 距離単位の詳細については、「 [**Ksk プロパティ\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)」を参照してください。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DBUFFER\_MINDISTANCE プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

サウンドソースからの最小距離を下回る距離では、距離が下がってもサウンドボリュームは大きくなりません。 DirectSound 3D バッファーの最小距離の詳細については、Microsoft Windows SDK のドキュメントで次の情報を参照してください。

-   DS3DBUFFER 構造体の**Flmindistance**メンバー。

-   **IDirectSound3DBuffer:: getmindistance**メソッドと**IDirectSound3DBuffer:: setmindistance**メソッド。

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

[**KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

 

 







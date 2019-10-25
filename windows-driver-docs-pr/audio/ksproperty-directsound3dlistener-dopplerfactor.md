---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR
description: KSK プロパティ\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR プロパティは、3D リスナーのドップラー係数を指定します。
ms.assetid: e07eb51f-6d87-4183-90cc-09bfa7523944
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14956c45b4c9d18a752cc2c228370f081806f51b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830765"
---
# <a name="ksproperty_directsound3dlistener_dopplerfactor"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR


KSK プロパティ\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR プロパティは、3D リスナーのドップラー係数を指定します。

## <span id="ddk_ksproperty_directsound3dlistener_dopplerfactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR_KS"></span>


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

 

プロパティ値 (操作データ) は FLOAT 型で、ドップラー係数を指定します。 ドップラー係数は、DS3D\_MINDOPPLERFACTOR から DS3D\_MAXDOPPLERFACTOR までの範囲になります。これは、それぞれ0.0 と10.0 として定義されています。 既定の要素は DS3D\_DEFAULTDOPPLERFACTOR で、1.0 として定義されています。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、3D リスナーと3D サウンドバッファーの両方に適用されるドップラー係数を指定します。

ドップラー係数が0の場合は、リスナーまたはサウンドバッファーの速度に関係なく、ドップラーシフトがサウンドに適用されないことを意味します。 1より大きい要素は、現実世界で発生するドップラーシフトの量を誇張します。

DirectSound は、このプロパティを使用して**IDirectSound3DListener:: GetDopplerFactor**メソッドと**IDirectSound3DListener:: SetDopplerFactor**メソッドを実装します。これについては、Microsoft Windows SDK のドキュメントを参照してください。

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

 

 







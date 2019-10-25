---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR
description: KSK プロパティ\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR プロパティは、3D リスナーのロールロール係数を指定します。
ms.assetid: 3eef80ef-921b-4364-b31d-14a62f305f5d
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR オーディオデバイス
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
ms.openlocfilehash: 3a2b7bec2c6d954cd194285108a6c64403d11ac0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832771"
---
# <a name="ksproperty_directsound3dlistener_rollofffactor"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR


KSK プロパティ\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR プロパティは、3D リスナーのロールロール係数を指定します。

## <span id="ddk_ksproperty_directsound3dlistener_rollofffactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR_KS"></span>


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

 

プロパティ値 (操作データ) は FLOAT 型で、ロールアウト係数を指定します。 ロールアウト係数は、DS3D\_MINROLLOFFFACTOR から DS3D\_MAXROLLOFFFACTOR までの範囲です。これは、それぞれ0.0 と10.0 として定義されています。 既定のロールアウト係数は DS3D\_DEFAULTROLLOFFFACTOR で、1.0 として定義されています。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

[ロールオフ] は、サウンドソースからのリスナーの距離に基づいて、サウンドに適用される減衰の量です。 ロールアウト率が0の場合は、リスナーからの距離に関係なく、サウンドに減衰が適用されないことを意味します。 1より大きい要素は、距離を持つサウンドの実際の減衰を誇張します。

DirectSound は、このプロパティを使用して**IDirectSound3DListener:: GetRolloffFactor**メソッドと**IDirectSound3DListener:: SetRolloffFactor**メソッドを実装します。これについては、Microsoft Windows SDK のドキュメントを参照してください。

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

 

 







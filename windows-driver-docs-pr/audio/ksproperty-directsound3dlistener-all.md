---
title: KSK プロパティ\_DIRECTSOUND3DLISTENER\_すべて
description: 指定したリスナー ID のすべての DirectSound 3D リスナーのプロパティを設定または取得するには、KSK プロパティ\_DIRECTSOUND3DLISTENER\_すべてのプロパティを使用します。
ms.assetid: cdf98ed6-cd8e-480c-b766-c348f41919ef
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALL オーディオデバイス
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
ms.openlocfilehash: 041310316c2e72a64327c0340d26e80a00e07791
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830809"
---
# <a name="ksproperty_directsound3dlistener_all"></a>KSK プロパティ\_DIRECTSOUND3DLISTENER\_すべて


指定したリスナー ID のすべての DirectSound 3D リスナーのプロパティを設定または取得するには、KSK プロパティ\_DIRECTSOUND3DLISTENER\_すべてのプロパティを使用します。

## <span id="ddk_ksproperty_directsound3dlistener_all_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ALL_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all" data-raw-source="[&lt;strong&gt;KSDS3D_LISTENER_ALL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all)"><strong>KSDS3D_LISTENER_ALL</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、3D リスナーのすべてのプロパティを指定する KSDS3D\_LISTENER 型の構造体\_ます。 この構造体は、Microsoft Windows SDK のドキュメントで説明されている DS3DBUFFER 構造体に似ています。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_DIRECTSOUND3DLISTENER\_すべてのプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

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

[**KSDS3D\_リスナー\_すべて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all)

 

 







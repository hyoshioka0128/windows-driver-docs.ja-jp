---
title: KSK プロパティ\_BDA\_シグナル\_存在する
description: クライアントは、\_BDA プロパティを使用して、シグナル通信事業者が存在するかどうかを判断するために、\_シグナル\_存在します。
ms.assetid: d3dbe0f7-a308-48e2-9751-0131fa2b512d
keywords:
- KSPROPERTY_BDA_SIGNAL_PRESENT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_PRESENT
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: be57094a5444494f78cb00978974f648924441d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842798"
---
# <a name="ksproperty_bda_signal_present"></a>KSK プロパティ\_BDA\_シグナル\_存在する


クライアントは、\_BDA プロパティを使用して、シグナル通信事業者が存在するかどうかを判断するために、\_シグナル\_存在します。

## <span id="ddk_ksproperty_bda_signal_present_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_PRESENT_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>ピン留めまたはフィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、コントロールノードの識別子を指定します。または、pin を指定するために−1に設定されています。

戻り値は、シグナル通信事業者が存在するかどうかを示します。 シグナルキャリアが存在する場合は**TRUE** 、それ以外の場合は**FALSE**を返します。 RF チューナーノードは、この表示を提供する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







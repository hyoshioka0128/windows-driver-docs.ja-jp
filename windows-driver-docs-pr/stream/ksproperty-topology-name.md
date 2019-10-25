---
title: KSK プロパティ\_トポロジ\_名
description: KSK プロパティ\_TOPOLOGY\_NAME プロパティは、ノードのローカライズされた Unicode 文字列名を提供します。
ms.assetid: ae12fe2f-9ccf-4949-b530-e7e33c846837
keywords:
- KSPROPERTY_TOPOLOGY_NAME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_NAME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6910f7fe0253dee1d7f99e2eb51b317b6fb2d021
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837923"
---
# <a name="ksproperty_topology_name"></a>KSK プロパティ\_トポロジ\_名


KSK プロパティ\_TOPOLOGY\_NAME プロパティは、ノードのローカライズされた Unicode 文字列名を提供します。

## <span id="ddk_ksproperty_topology_name_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_NAME_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>ノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node" data-raw-source="[&lt;strong&gt;KSP_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)"><strong>KSP_NODE</strong></a></p></td>
<td><p>文字列名を保持するバッファー。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP\_ノード構造の**NodeId**メンバーは、文字列名を返すノード ID を指定します。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







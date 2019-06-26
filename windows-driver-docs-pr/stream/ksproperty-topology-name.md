---
title: KSPROPERTY\_トポロジ\_名
description: KSPROPERTY\_トポロジ\_NAME プロパティは、ノードのローカライズされた Unicode 文字列名を提供します。
ms.assetid: ae12fe2f-9ccf-4949-b530-e7e33c846837
keywords:
- KSPROPERTY_TOPOLOGY_NAME ストリーミング メディア デバイス
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
ms.openlocfilehash: b5ad8749c393243fc02c2702a00ac9cab13d4231
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383995"
---
# <a name="kspropertytopologyname"></a>KSPROPERTY\_トポロジ\_名


KSPROPERTY\_トポロジ\_NAME プロパティは、ノードのローカライズされた Unicode 文字列名を提供します。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>ノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node" data-raw-source="[&lt;strong&gt;KSP_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)"><strong>KSP_NODE</strong></a></p></td>
<td><p>文字列名を保持するバッファー。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノード構造は、文字列名を返す対象のノード ID を指定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 







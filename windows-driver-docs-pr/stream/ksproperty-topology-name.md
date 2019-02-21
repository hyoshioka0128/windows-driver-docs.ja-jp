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
ms.openlocfilehash: b2e24e108230a506754bc8a2f53bba9a9e8634c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528222"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566720" data-raw-source="[&lt;strong&gt;KSP_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566720)"><strong>KSP_NODE</strong></a></p></td>
<td><p>文字列名を保持するバッファー。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノード構造は、文字列名を返す対象のノード ID を指定します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 







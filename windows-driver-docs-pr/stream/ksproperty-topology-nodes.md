---
title: KSPROPERTY\_トポロジ\_ノード
description: KSPROPERTY\_トポロジ\_ノードがフィルターでサポートされている Guid の種類、トポロジのノードとノードの一覧を提供します。
ms.assetid: 3b07b4d5-b222-44f1-be62-3addf3a87847
keywords:
- KSPROPERTY_TOPOLOGY_NODES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_NODES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd4a3e8468d9b22db56da3f75484c50143652d01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384145"
---
# <a name="kspropertytopologynodes"></a>KSPROPERTY\_トポロジ\_ノード


KSPROPERTY\_トポロジ\_ノードがフィルターでサポートされている Guid の種類、トポロジのノードとノードの一覧を提供します。

## <span id="ddk_ksproperty_topology_nodes_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_NODES_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>A <a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"> <strong>KSMULTIPLE_ITEM</strong> </a>一連の Guid の後に、構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

GUID の一覧は、ノードの種類を表します。 シーケンス内のインデックスは、ノードの ID 番号と一致する必要があります。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

 

 







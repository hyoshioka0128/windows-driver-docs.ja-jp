---
title: KSPROPERTY\_BDA\_ノード\_型
description: クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードの種類の一覧を取得する型。
ms.assetid: 8fe72434-3635-4c2c-a72a-1fd398e488d8
keywords:
- KSPROPERTY_BDA_NODE_TYPES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_TYPES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 590dbb0659bf11f36f85d3404d9c87175352bf70
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386915"
---
# <a name="kspropertybdanodetypes"></a>KSPROPERTY\_BDA\_ノード\_型


クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードの種類の一覧を取得する型。

## <span id="ddk_ksproperty_bda_node_types_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_TYPES_KS"></span>


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
<td><p>KSPROPERTY</p></td>
<td><p>KSNODE_DESCRIPTORs の一覧</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

テンプレートのトポロジで各ノードの種類は 1 回だけが、実際のトポロジで複数回が発生することができます。 このノードの種類の一覧が KSNODE の配列\_記述子構造体。 通常、この配列内の各要素のインデックスは、各ノード タイプを識別するために使用されます。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyNodeTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertynodetypes)

[**KSNODE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksnode_descriptor)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 







---
title: KSK プロパティ\_BDA\_ノード\_型
description: クライアントは、ノードの種類の一覧を取得するために、KSK プロパティ\_BDA\_ノード\_型を使用します。
ms.assetid: 8fe72434-3635-4c2c-a72a-1fd398e488d8
keywords:
- KSPROPERTY_BDA_NODE_TYPES ストリーミングメディアデバイス
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
ms.openlocfilehash: 1e9edfbc59d070987e4f532bdaf129f323c07fe8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844342"
---
# <a name="ksproperty_bda_node_types"></a>KSK プロパティ\_BDA\_ノード\_型


クライアントは、ノードの種類の一覧を取得するために、KSK プロパティ\_BDA\_ノード\_型を使用します。

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
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>KSNODE_DESCRIPTORs の一覧</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

テンプレートトポロジでは、各ノードタイプは1回しか実行できませんが、実際のトポロジでは複数回発生する可能性があります。 このノード型の一覧は、KSK ノード\_記述子の構造体の配列です。 通常、この配列内の各要素のインデックスは、特定のノード型を識別するために使用されます。

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


[**BdaPropertyNodeTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodetypes)

[**KSNODE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 







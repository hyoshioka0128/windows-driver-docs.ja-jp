---
title: KSPROPERTY\_BDA\_ノード\_記述子
description: クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードの一覧を取得する記述子。
ms.assetid: 53b297e6-7e31-4231-80ad-b114cf9343b4
keywords:
- KSPROPERTY_BDA_NODE_DESCRIPTORS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_DESCRIPTORS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40233969906bea261bb1e6229398b21687a2e4fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373735"
---
# <a name="kspropertybdanodedescriptors"></a>KSPROPERTY\_BDA\_ノード\_記述子


クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードの一覧を取得する記述子。

## <span id="ddk_ksproperty_bda_node_descriptors_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_DESCRIPTORS_KS"></span>


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
<td><p>Guid のリスト</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ノードの一覧は、使用可能なノードの Guid の配列です。

テンプレートのトポロジでの作成に使用できる BDA ノードの一覧は、次を参照してください。 [BDA ノード カテゴリ Guid](bda-node-category-guids.md)します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyNodeDescriptors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertynodedescriptors)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 







---
title: KSPROPERTY\_BDA\_ノード\_プロパティ
description: クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードでサポートされるプロパティの一覧を取得するプロパティ。
ms.assetid: 36d37844-a69b-4f67-bb8f-e5445ba9a2cb
keywords:
- KSPROPERTY_BDA_NODE_PROPERTIES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_PROPERTIES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d304764b28cb186446db9ba86869b213d8f6c44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376668"
---
# <a name="kspropertybdanodeproperties"></a>KSPROPERTY\_BDA\_ノード\_プロパティ


クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードでサポートされるプロパティの一覧を取得するプロパティ。

## <span id="ddk_ksproperty_bda_node_properties_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_PROPERTIES_KS"></span>


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

ノードでサポートされるプロパティの一覧は、Guid の一覧を示します。

ネットワーク プロバイダーでは、このプロパティを使用して、BDA テンプレートの接続リスト内の各ノードの機能のクエリを実行します。

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


[**BdaPropertyNodeProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertynodeproperties)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 







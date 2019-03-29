---
title: KSPROPERTY\_セレクター\_ソース\_ノード\_ID
description: KSPROPERTY\_セレクター\_ソース\_ノード\_ID プロパティは、特定のノードのソースの pin の pin 識別子を指定します。
ms.assetid: 7616e834-462c-4e2c-8a4f-ec20db042e3b
keywords:
- KSPROPERTY_SELECTOR_SOURCE_NODE_ID ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SELECTOR_SOURCE_NODE_ID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0da81f86176e7dd852eaca13b3c159738df3786
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582531"
---
# <a name="kspropertyselectorsourcenodeid"></a>KSPROPERTY\_セレクター\_ソース\_ノード\_ID


KSPROPERTY\_セレクター\_ソース\_ノード\_ID プロパティは、特定のノードのソースの pin の pin 識別子を指定します。

## <span id="ddk_ksproperty_selector_source_node_id_ks"></span><span id="DDK_KSPROPERTY_SELECTOR_SOURCE_NODE_ID_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565219" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565219)"><strong>KSPROPERTY_SELECTOR_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff565217" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565217)"> <strong>KSPROPERTY_SELECTOR_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

クライアントで有効な pin 識別子を指定する必要がありますセット要求を行うときに、**値**プロパティ記述子構造体のメンバー。

クライアントがで pin 識別子を受け取る get 要求を行うときに、**値**プロパティ記述子構造体のメンバー。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 






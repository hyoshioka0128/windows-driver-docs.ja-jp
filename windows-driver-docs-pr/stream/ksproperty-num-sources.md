---
title: '\_ソースに\_KSK プロパティ'
description: KSK プロパティ\_NUM\_SOURCES プロパティは、セレクター単位の入力ピンの数を指定します。
ms.assetid: 94d0f926-0551-4fe2-aa7f-2898e04c4b36
keywords:
- KSPROPERTY_NUM_SOURCES ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_NUM_SOURCES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8973dc2fe5519036dc3fb3bdb4d6ef312bfb3099
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842752"
---
# <a name="ksproperty_num_sources"></a>\_ソースに\_KSK プロパティ


KSK プロパティ\_NUM\_SOURCES プロパティは、セレクター単位の入力ピンの数を指定します。

## <span id="ddk_ksproperty_num_sources_ks"></span><span id="DDK_KSPROPERTY_NUM_SOURCES_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_s)"><strong>KSPROPERTY_SELECTOR_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_node_s)"> <strong>KSPROPERTY_SELECTOR_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Get 要求を行うと、クライアントは、プロパティ記述子構造の**Value**メンバー内の使用可能なソース pin の数を受け取ります。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

 

 






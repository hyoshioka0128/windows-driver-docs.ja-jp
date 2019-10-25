---
title: KSK プロパティ\_BDA\_TABLE\_セクション
description: クライアントは、KSK プロパティ\_BDA\_TABLE\_SECTION を使用して、ノードの出力にデータを配信するときに使用するテーブルセクションをノードに通知します。
ms.assetid: 58e6cc37-b6f1-49d6-a832-46f1edabf740
keywords:
- KSPROPERTY_BDA_TABLE_SECTION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TABLE_SECTION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02b62d7ef8bead5c609246930c5c56182fba727
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843598"
---
# <a name="ksproperty_bda_table_section"></a>KSK プロパティ\_BDA\_TABLE\_セクション


クライアントは、KSK プロパティ\_BDA\_TABLE\_SECTION を使用して、ノードの出力にデータを配信するときに使用するテーブルセクションをノードに通知します。

## <span id="ddk_ksproperty_bda_table_section_ks"></span><span id="DDK_KSPROPERTY_BDA_TABLE_SECTION_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>BDA_TABLE_SECTION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、lnb アンプノードを指定します。

BDA\_TABLE\_セクション構造では、table セクションについて説明します。

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


[**BDA\_テーブル\_セクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_table_section)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







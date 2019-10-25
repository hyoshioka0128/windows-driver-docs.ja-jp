---
title: KSK プロパティ\_BDA\_CA\_\_プログラムを削除します
description: クライアントは、KSK プロパティ\_BDA\_CA を使用して\_プログラム\_削除し、特定のプログラムにアクセスできないようにします。
ms.assetid: 07792113-6d47-4836-8db2-6960fb14ab87
keywords:
- KSPROPERTY_BDA_CA_REMOVE_PROGRAM ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_REMOVE_PROGRAM
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ae0ea5d5039c6ecce027e553154aa068418e7e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842150"
---
# <a name="ksproperty_bda_ca_remove_program"></a>KSK プロパティ\_BDA\_CA\_\_プログラムを削除します


クライアントは、KSK プロパティ\_BDA\_CA を使用して\_プログラム\_削除し、特定のプログラムにアクセスできないようにします。

## <span id="ddk_ksproperty_bda_ca_remove_program_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_REMOVE_PROGRAM_KS"></span>


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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティ値は、アクセスできないようにするプログラムを指定します。

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


[**KSEVENT\_BDA\_プログラム\_フロー\_状態\_変更されました**](ksevent-bda-program-flow-status-changed.md)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







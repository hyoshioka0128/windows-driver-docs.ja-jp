---
title: KSK プロパティ\_BDA\_外部\_FEC\_型
description: クライアントは、KSK プロパティ\_BDA\_OUTER\_FEC\_TYPE を使用して、demodulator ノードの外部前方エラー修正 (FEC) 型を制御します。
ms.assetid: 952fd2d6-20c8-4fb3-a92a-1e6bcedfd68b
keywords:
- KSPROPERTY_BDA_OUTER_FEC_TYPE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_OUTER_FEC_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f83a3e7d13303067f27c8efbce04a671ec5f1f53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837615"
---
# <a name="ksproperty_bda_outer_fec_type"></a>KSK プロパティ\_BDA\_外部\_FEC\_型


クライアントは、KSK プロパティ\_BDA\_OUTER\_FEC\_TYPE を使用して、demodulator ノードの外部前方エラー修正 (FEC) 型を制御します。

## <span id="ddk_ksproperty_bda_outer_fec_type_ks"></span><span id="DDK_KSPROPERTY_BDA_OUTER_FEC_TYPE_KS"></span>


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
<td><p>FECMethod</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

FECMethod 列挙型から返された値は、FEC 型を識別します。

KSP の**NodeId**メンバー\_node は、demodulator ノードの識別子を指定します。

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


[**FECMethod**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/fecmethod)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







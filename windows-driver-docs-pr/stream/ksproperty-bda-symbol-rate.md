---
title: KSK プロパティ\_BDA\_シンボル\_率
description: クライアントは、KSK プロパティ\_BDA\_SYMBOL\_RATE を使用して、demodulator ノードのシンボルレートを制御します。
ms.assetid: 11e2e020-3037-4a68-a8d6-c68efd86a518
keywords:
- KSPROPERTY_BDA_SYMBOL_RATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SYMBOL_RATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb05cfa5e84cd89eca55808a8e107893148fe2c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843599"
---
# <a name="ksproperty_bda_symbol_rate"></a>KSK プロパティ\_BDA\_シンボル\_率


クライアントは、KSK プロパティ\_BDA\_SYMBOL\_RATE を使用して、demodulator ノードのシンボルレートを制御します。

## <span id="ddk_ksproperty_bda_symbol_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_SYMBOL_RATE_KS"></span>


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

戻り値は、シンボルレートを指定します。

KSP の**NodeId**メンバー\_node は、demodulator ノードの識別子を指定します。

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







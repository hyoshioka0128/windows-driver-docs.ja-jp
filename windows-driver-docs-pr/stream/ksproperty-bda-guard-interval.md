---
title: KSK プロパティ\_BDA\_ガード\_INTERVAL
description: クライアントは、KSK プロパティ\_BDA\_GUARD\_INTERVAL を使用して、demodulator ノードのガード間隔の設定を制御します。
ms.assetid: 7c0c6c5e-94fd-4013-9778-d41568ae9f0b
keywords:
- KSPROPERTY_BDA_GUARD_INTERVAL ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_GUARD_INTERVAL
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18fe020a72eae161a2b2f705b5563fabac75d12f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842142"
---
# <a name="ksproperty_bda_guard_interval"></a>KSK プロパティ\_BDA\_ガード\_INTERVAL


クライアントは、KSK プロパティ\_BDA\_GUARD\_INTERVAL を使用して、demodulator ノードのガード間隔の設定を制御します。

## <span id="ddk_ksproperty_bda_guard_interval_ks"></span><span id="DDK_KSPROPERTY_BDA_GUARD_INTERVAL_KS"></span>


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
<td><p>Guシャード間隔</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Guシャード間隔列挙型から返された値は、ガード間隔の設定を識別します。

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


[**Guシャード間隔**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/guardinterval)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







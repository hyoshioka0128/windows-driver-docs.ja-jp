---
title: KSPROPERTY\_BDA\_CA\_スマート\_カード\_状態
description: クライアントを使用して、KSPROPERTY\_BDA\_CA\_スマート\_カード\_ECM のマップ ノードに関連付けられているスマート カード リーダーの状態を確認する状態。
ms.assetid: a53cea17-0463-4909-839b-6e8ad67dac82
keywords:
- KSPROPERTY_BDA_CA_SMART_CARD_STATUS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_SMART_CARD_STATUS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 845accb5a1f67f66c2d442177270d6f0eabd32bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364880"
---
# <a name="kspropertybdacasmartcardstatus"></a>KSPROPERTY\_BDA\_CA\_スマート\_カード\_状態


クライアントを使用して、KSPROPERTY\_BDA\_CA\_スマート\_カード\_ECM のマップ ノードに関連付けられているスマート カード リーダーの状態を確認する状態。

## <span id="ddk_ksproperty_bda_ca_smart_card_status_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_SMART_CARD_STATUS_KS"></span>


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
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

返される値は、スマート カード リーダーの状態を指定します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSEVENT\_BDA\_CA\_スマート\_カード\_状態\_CHANGED**](ksevent-bda-ca-smart-card-status-changed.md)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 







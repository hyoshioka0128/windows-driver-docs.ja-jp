---
title: KSK プロパティ\_BDA\_CA\_モジュール\_の状態
description: クライアントは、KSK プロパティ\_BDA\_CA\_モジュール\_ステータスを使用して、ECM マップノードに関連付けられている CA モジュールの状態を確認します。
ms.assetid: 4bd8a423-7a76-4702-a769-0de88fcc5772
keywords:
- KSPROPERTY_BDA_CA_MODULE_STATUS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_MODULE_STATUS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 825bbe174c7df9d332ba9afca9ff712d5b8b5f70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842154"
---
# <a name="ksproperty_bda_ca_module_status"></a>KSK プロパティ\_BDA\_CA\_モジュール\_の状態


クライアントは、KSK プロパティ\_BDA\_CA\_モジュール\_ステータスを使用して、ECM マップノードに関連付けられている CA モジュールの状態を確認します。

## <span id="ddk_ksproperty_bda_ca_module_status_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_MODULE_STATUS_KS"></span>


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

返される値は、CA モジュールの状態を指定します。

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


[**KSEVENT\_BDA\_CA\_モジュール\_状態\_変更**](ksevent-bda-ca-module-status-changed.md)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







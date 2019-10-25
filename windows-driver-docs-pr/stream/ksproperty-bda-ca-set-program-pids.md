---
title: KSK プロパティ\_BDA\_CA\_設定\_プログラム\_PID
description: クライアントは、KSK プロパティ\_BDA\_CA を使用\_\_プログラム\_PID を設定して、特定のプログラムのパケット識別子の一覧を設定します。
ms.assetid: 5cc049f7-df97-4739-8ec4-22ab646781a6
keywords:
- KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd6131bbc58139e9c0866d91d1ef032469938202
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842157"
---
# <a name="ksproperty_bda_ca_set_program_pids"></a>KSK プロパティ\_BDA\_CA\_設定\_プログラム\_PID


クライアントは、KSK プロパティ\_BDA\_CA を使用\_\_プログラム\_PID を設定して、特定のプログラムのパケット識別子の一覧を設定します。

## <span id="ddk_ksproperty_bda_ca_set_program_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS_KS"></span>


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
<td><p>BDA_PROGRAM_PID_LIST</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA\_プログラム\_PID\_LIST 構造体には、指定したプログラムのパケット識別子の一覧が含まれています。

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


[**BDA\_プログラム\_PID\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_program_pid_list)

[**KSEVENT\_BDA\_プログラム\_フロー\_状態\_変更されました**](ksevent-bda-program-flow-status-changed.md)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







---
title: KSK プロパティ\_BDA\_PIDFILTER\_リスト\_PID
description: クライアントは、KSK プロパティ\_BDA\_PIDFILTER\_\_リストを使用して PID フィルターノードから取得します。これは、ノードが入力ストリームから出力ストリームに配信するパケットのグループを識別する pid の一覧です。
ms.assetid: fc7dc0af-af74-4bd1-b99c-f06de25aae3c
keywords:
- KSPROPERTY_BDA_PIDFILTER_LIST_PIDS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIDFILTER_LIST_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc7ddeb9eb904fcc5e6ba24c6c5da1cb3d7385d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837613"
---
# <a name="ksproperty_bda_pidfilter_list_pids"></a>KSK プロパティ\_BDA\_PIDFILTER\_リスト\_PID


クライアントは、KSK プロパティ\_BDA\_PIDFILTER\_\_リストを使用して PID フィルターノードから取得します。これは、ノードが入力ストリームから出力ストリームに配信するパケットのグループを識別する pid の一覧です。

## <span id="ddk_ksproperty_bda_pidfilter_list_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_LIST_PIDS_KS"></span>


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
<td><p>Pid の一覧</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、PID フィルターノードの識別子を指定します。

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


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







---
title: KSK プロパティ\_BDA\_PIDFILTER\_マップ解除\_PID
description: クライアントは、KSK プロパティ\_BDA\_PIDFILTER\_\_使用して、PID フィルターノードに、特定の Pid で識別されたパケットについての入力ストリームからのフィルター処理 (つまり、入力から出力への渡しを停止) について通知します。
ms.assetid: 111d8857-84f4-4a7f-8771-ea6537c4c592
keywords:
- KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68fa8e43a950b09cdc379c0f473ce8ce6a96b717
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837607"
---
# <a name="ksproperty_bda_pidfilter_unmap_pids"></a>KSK プロパティ\_BDA\_PIDFILTER\_マップ解除\_PID


クライアントは、KSK プロパティ\_BDA\_PIDFILTER\_\_使用して、PID フィルターノードに、特定の Pid で識別されたパケットについての入力ストリームからのフィルター処理 (つまり、入力から出力への渡しを停止) について通知します。

## <span id="ddk_ksproperty_bda_pidfilter_unmap_pids_ks"></span><span id="DDK_KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS_KS"></span>


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
<td><p>BDA_PID_UNMAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、PID フィルターノードの識別子を指定します。

BDA\_PID\_構造のマップ解除では、入力ストリームからフィルター処理するために特定の Pid で識別されるパケットのマップを記述します。

この一覧に含まれる、ノードによって渡されない PID はすべて無視されます。

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


[**BDA\_PID\_マップ解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_pid_unmap)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

 

 







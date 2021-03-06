---
title: KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PID
description: クライアントを使用して、KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PID PID を通知するために特定の Pid を入力ストリームからフィルターで識別されるパケットのノードをフィルター処理 (つまり、停止出力への入力からを渡すこと)。
ms.assetid: 111d8857-84f4-4a7f-8771-ea6537c4c592
keywords:
- KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS ストリーミング メディア デバイス
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
ms.openlocfilehash: cedcdc9313dc92ab04ed53bd3d77cd4455fdd982
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368152"
---
# <a name="kspropertybdapidfilterunmappids"></a>KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PID


クライアントを使用して、KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PID PID を通知するために特定の Pid を入力ストリームからフィルターで識別されるパケットのノードをフィルター処理 (つまり、停止出力への入力からを渡すこと)。

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
<td><p>BDA_PID_UNMAP</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードが PID フィルター ノードの識別子を指定します。

BDA\_PID\_UNMAP 構造体には、特定の Pid を入力ストリームからフィルターで識別されるパケットのマップがについて説明します。

ノードでは渡されませんがリスト内の任意の PID は無視されます。

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


[**BDA\_PID\_マッピング解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdatypes/ns-bdatypes-_bda_pid_unmap)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 







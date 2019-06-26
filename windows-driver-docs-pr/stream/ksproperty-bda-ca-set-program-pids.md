---
title: KSPROPERTY\_BDA\_CA\_設定\_プログラム\_PID
description: クライアントを使用して、KSPROPERTY\_BDA\_CA\_設定\_プログラム\_PID パケット識別子の一覧を特定のプログラムで設定します。
ms.assetid: 5cc049f7-df97-4739-8ec4-22ab646781a6
keywords:
- KSPROPERTY_BDA_CA_SET_PROGRAM_PIDS ストリーミング メディア デバイス
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
ms.openlocfilehash: 1d15d6d1cac90709fa45414ace31a5f8f223065a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364892"
---
# <a name="kspropertybdacasetprogrampids"></a>KSPROPERTY\_BDA\_CA\_設定\_プログラム\_PID


クライアントを使用して、KSPROPERTY\_BDA\_CA\_設定\_プログラム\_PID パケット識別子の一覧を特定のプログラムで設定します。

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
<td><p>BDA_PROGRAM_PID_LIST</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA\_プログラム\_PID\_リスト構造体には、パケットの識別子を指定したプログラムの一覧が含まれています。

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


[**BDA\_プログラム\_PID\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdatypes/ns-bdatypes-_bda_program_pid_list)

[**KSEVENT\_BDA\_プログラム\_フロー\_状態\_CHANGED**](ksevent-bda-program-flow-status-changed.md)

[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 







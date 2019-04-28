---
title: NdisOidComplete ルール (ndis)
description: NdisOidComplete ルールは、NDIS ミニポート ドライバーが、OID を正しく完了したことを確認します。
ms.assetid: 344DECA8-F72A-4962-80D0-DDC648A4FC21
ms.date: 05/21/2018
keywords:
- NdisOidComplete ルール (ndis)
topic_type:
- apiref
api_name:
- NdisOidComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77817c2f6f7432f955f020ddabfaef0f9de36fca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360764"
---
# <a name="ndisoidcomplete-rule-ndis"></a>NdisOidComplete ルール (ndis)


**NdisOidComplete**ルールは、NDIS ミニポート ドライバーが、OID を正しく完了したことを確認します。

ミニポート ドライバーには、許容される NTSTATUS 値を持つ OID 要求操作を完了する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">OID の場合。</th>
<th align="left">次の NTSTATUS 値でのみ完了できます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OID_PNP_SET_POWER</p></td>
<td align="left"><p>NDIS_STATUS_NOT_ACCEPTED</p>
<p>NDIS_STATUS_SUCCESS</p>
<p>NDIS_STATUS_PENDING</p></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER</p>
<p>OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA</p>
<p>OID_RECEIVE_FILTER_FREE_QUEUE</p>
<p>OID_NIC_SWITCH_FREE_VF</p>
<p>OID_NIC_SWITCH_DELETE_SWITCH</p>
<p>OID_802_3_DELETE_MULTICAST_ADDRESS</p>
<p>OID_PM_REMOVE_WOL_PATTERN</p>
<p>OID_PM_REMOVE_PROTOCOL_OFFLOAD</p>
<p>OID_TUNNEL_INTERFACE_RELEASE_OID</p></td>
<td align="left"><p>NDIS_STATUS_NOT_ACCEPTED</p>
<p>NDIS_STATUS_REQUEST_ABORTED</p>
<p>NDIS_STATUS_SUCCESS</p>
<p>NDIS_STATUS_PENDING</p></td>
</tr>
</tbody>
</table>

 

ミニポート ドライバーを呼び出してはならない、 [ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622) NDIS として要求操作の最終的な状態で関数を\_状態\_保留します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">さらに、OID がの場合。</th>
<th align="left">次の NTSTATUS 値でのみ完了できます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OID_PNP_SET_POWER</p></td>
<td align="left"><p>NDIS_STATUS_NOT_ACCEPTED</p>
<p>NDIS_STATUS_SUCCESS</p></td>
</tr>
<tr class="even">
<td align="left"><p>OID_RECEIVE_FILTER_CLEAR_FILTER</p>
<p>OID_TCP_TASK_IPSEC_OFFLOAD_V2_DELETE_SA</p>
<p>OID_RECEIVE_FILTER_FREE_QUEUE</p>
<p>OID_NIC_SWITCH_FREE_VF</p>
<p>OID_NIC_SWITCH_DELETE_SWITCH</p>
<p>OID_802_3_DELETE_MULTICAST_ADDRESS</p>
<p>OID_PM_REMOVE_WOL_PATTERN</p>
<p>OID_PM_REMOVE_PROTOCOL_OFFLOAD</p>
<p>OID_TUNNEL_INTERFACE_RELEASE_OID</p></td>
<td align="left"><p>NDIS_STATUS_NOT_ACCEPTED</p>
<p>NDIS_STATUS_REQUEST_ABORTED</p>
<p>NDIS_STATUS_SUCCESS</p></td>
</tr>
</tbody>
</table>

 

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00091001) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 検証</a>オプション。 このルールはでテストされても、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**MiniportDevicePnPEventNotify**](https://msdn.microsoft.com/library/windows/hardware/ff559369)
[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 

 






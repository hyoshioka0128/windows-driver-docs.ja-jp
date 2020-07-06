---
title: NdisOidComplete rule (ndis)
description: NdisOidComplete ルールは、NDIS ミニポートドライバーが OID を正しく完了したことを確認します。
ms.assetid: 344DECA8-F72A-4962-80D0-DDC648A4FC21
ms.date: 05/21/2018
keywords:
- NdisOidComplete rule (ndis)
topic_type:
- apiref
api_name:
- NdisOidComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3532795a5ee62d5b4e0c990a6399aca82c73ce7b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968095"
---
# <a name="ndisoidcomplete-rule-ndis"></a>NdisOidComplete rule (ndis)


**NdisOidComplete**ルールは、NDIS ミニポートドライバーが OID を正しく完了したことを確認します。

ミニポートドライバーは、許可されている NTSTATUS 値を使用して OID 要求操作を完了する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">OID が次の場合:</th>
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

 

ミニポートドライバーは、要求操作[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)の最終ステータスが \_ "NDIS status PENDING" である NdisMOidRequestComplete 関数を呼び出すことはできません \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">さらに、OID が次のようになります。</th>
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

 

**ドライバーモデル: NDIS**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツールの \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00091001)


<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプションを選択します。 このルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>オプションを使用してもテストされます。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**MiniportDevicePnPEventNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify) 
[**Miniportoidrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)
 

 






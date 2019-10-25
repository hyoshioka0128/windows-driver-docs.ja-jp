---
title: NDIS/WIFI 検証の規則セット
description: 注 Windows 8.1 で始まるこれらの規則を使用して、NDIS/WIFI ドライバーをテストすることができます。 .
ms.assetid: B856F42E-E4AD-4178-AF71-3E68A23209C9
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f7ece175abda9d298922787cd24f4ce34187d3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840072"
---
# <a name="ndiswifi-verification-rule-set"></a>NDIS/WIFI 検証の規則セット


> [!NOTE]
> これらのルールを使用して、Windows 8.1 で始まる NDIS/WIFI ドライバーをテストできます。

 

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndisfiltertimeddatareceive.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataReceive&lt;/strong&gt;](ndisfiltertimeddatareceive.md)"><strong>NdisFilterTimedDataReceive</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimeddatareceive.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataReceive&lt;/strong&gt;](ndisfiltertimeddatareceive.md)"><strong>NdisFilterTimedDataReceive</strong></a>規則は、NDIS フィルタードライバーが、タイムアウトする前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists" data-raw-source="[&lt;em&gt;FilterReceiveNetBufferLists&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)"><em>FilterReceiveNetBufferLists</em></a>関数によって受信要求を完了することを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"><strong>NdisFilterTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"><strong>NdisFilterTimedDataSend</strong></a>規則は、NDIS フィルタードライバーが、タイムアウトする前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists" data-raw-source="[&lt;em&gt;FilterSendNetBufferLists&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)"><em>filtersendnetbufferlists</em></a>関数によって送信要求を完了することを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"><strong>NdisFilterTimedPauseComplete</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"><strong>NdisFilterTimedPauseComplete</strong></a>は次の3つのことを確認します。</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)"><em>Filterpause</em></a>関数は10秒以内に完了します。</p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)"><em>Filterpause</em></a>関数は失敗しません。</p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)"><em>Filterpause</em></a>関数を2回完了することはできません。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"><strong>NdisOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"><strong>NdisOidComplete</strong></a>ルールは、NDIS ミニポートドライバーが OID を正しく完了したことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"><strong>NdisOidDoubleComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"><strong>NdisOidDoubleComplete</strong></a>規則は、NDIS ミニポートドライバーが同じ OID に対して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>ルーチンを2回呼び出すことができないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"><strong>NdisOidDoubleRequest</strong></a></p></td>
<td align="left"><p>この<a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"><strong>NdisOidDoubleRequest</strong></a>ルールでは、次のことを確認します。</p>
<ul>
<li><p>Minport ドライバーは、現在保留中の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>を完了する必要があります。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"><strong>NdisTimedDataHang</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"><strong>NdisTimedDataHang</strong></a>ルールは、NDIS ミニポートドライバーが、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list" data-raw-source="[&lt;strong&gt;NET_BUFFER_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)"><strong>NET_BUFFER_LIST</strong></a>構造に対する保留中の送信要求を22秒以内に処理することを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"><strong>NdisTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"><strong>NdisTimedDataSend</strong></a>ルールは、NDIS ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists" data-raw-source="[&lt;em&gt;MiniportSendNetBufferLists&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)"><em>Miniportsendnetbufferlists</em></a>を呼び出すと、ミニポートドライバーが30秒以内に送信要求を完了することを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"><strong>NdisTimedOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"><strong>NdisTimedOidComplete</strong></a>規則は、NDIS ミニポートドライバーが、12秒以内に OID 要求を完了することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"><strong>WlanAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"><strong>WlanAssociation</strong></a>ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) アソシエーションシーケンスに従っていることを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"><strong>WlanConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"><strong>WlanConnectionRoaming</strong></a>ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 接続とローミングシーケンスに正しく従っていることを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"><strong>WlanDisassociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"><strong>WlanDisassociation</strong></a>ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 関連付けシーケンスに正しく従っていることを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"><strong>WlanTimedAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"><strong>WlanTimedAssociation</strong></a>規則は、NDIS ミニポートドライバーが10秒以内にワイヤレス LAN (WLAN) の関連付け操作を完了することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"><strong>WlanTimedConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"><strong>WlanTimedConnectionRoaming</strong></a>規則は、NDIS ミニポートドライバーが10秒以内にワイヤレス LAN (WLAN) 接続/ローミング操作を完了することを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"><strong>WlanTimedConnectRequest</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"><strong>WlanTimedConnectRequest</strong></a>ルールは、OID_DOT11_CONNECT_REQUEST の後に10秒以内に NDIS_STATUS_DOT11_CONNECTION_START が続くことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"><strong>WlanTimedScan</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"><strong>WlanTimedScan</strong></a>ルールは、WLAN スキャン操作が15秒以内に完了したことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"><strong>WlanTimedLinkQuality</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"><strong>WlanTimedLinkQuality</strong></a>ルールでは、NDIS_STATUS_DOT11_ASSOCIATION_COMPLETION が成功してから15秒後に NDIS_STATUS_DOT11_LINK_QUALITY が示されることを指定します。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

 

 






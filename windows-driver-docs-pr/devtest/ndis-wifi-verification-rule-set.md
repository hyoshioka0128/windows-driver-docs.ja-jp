---
title: NDIS/WIFI 検証の規則セット
description: Windows 8.1 以降、これらの規則で NDIS/WIFI ドライバーをテストすることができますに注意してください。 .
ms.assetid: B856F42E-E4AD-4178-AF71-3E68A23209C9
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 99842313e9f8432af57ef009df1648ad8aaac86e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374681"
---
# <a name="ndiswifi-verification-rule-set"></a>NDIS/WIFI 検証の規則セット


> [!NOTE]
> Windows 8.1 以降、これらのルールでは、NDIS/WIFI ドライバーをテストできます。

 

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
<td align="left"><p><a href="ndisfiltertimeddatareceive.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataReceive&lt;/strong&gt;](ndisfiltertimeddatareceive.md)"> <strong>NdisFilterTimedDataReceive</strong> </a>ルールでは、NDIS フィルター ドライバーが、受信要求が完了したことを検証、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549960" data-raw-source="[&lt;em&gt;FilterReceiveNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549960)"> <em>FilterReceiveNetBufferLists</em></a>タイムアウトになるまでの関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"><strong>NdisFilterTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedDataSend&lt;/strong&gt;](ndisfiltertimeddatasend.md)"> <strong>NdisFilterTimedDataSend</strong> </a>ルールでは、NDIS フィルター ドライバーが、送信要求が完了したことを検証、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549966" data-raw-source="[&lt;em&gt;FilterSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549966)"> <em>FilterSendNetBufferLists</em> </a>タイムアウトになるまでの関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"><strong>NdisFilterTimedPauseComplete</strong></a></p></td>
<td align="left"><p><a href="ndisfiltertimedpausecomplete-.md" data-raw-source="[&lt;strong&gt;NdisFilterTimedPauseComplete&lt;/strong&gt;](ndisfiltertimedpausecomplete-.md)"> <strong>NdisFilterTimedPauseComplete</strong> </a> 3 つのことを確認します。</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549957" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549957)"> <em>FilterPause</em> </a>関数は、10 秒後に完了した以下になります。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549957" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549957)"> <em>FilterPause</em> </a>関数が成功する必要があります。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549957" data-raw-source="[&lt;em&gt;FilterPause&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549957)"> <em>FilterPause</em> </a>関数を 2 回完了する必要がありますできません。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"><strong>NdisOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisOidComplete&lt;/strong&gt;](ndis-ndisoidcomplete.md)"> <strong>NdisOidComplete</strong> </a>ルールは、NDIS ミニポート ドライバーが、OID を正しく完了したことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"><strong>NdisOidDoubleComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisoiddoublecomplete.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleComplete&lt;/strong&gt;](ndis-ndisoiddoublecomplete.md)"> <strong>NdisOidDoubleComplete</strong> </a>ルールでは、NDIS ミニポート ドライバーを呼び出してはならないことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563622" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563622)"> <strong>NdisMOidRequestComplete</strong> </a>同じ OID の 2 回ルーチンです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"><strong>NdisOidDoubleRequest</strong></a></p></td>
<td align="left"><p>これは、 <a href="ndis-ndisoiddoublerequest.md" data-raw-source="[&lt;strong&gt;NdisOidDoubleRequest&lt;/strong&gt;](ndis-ndisoiddoublerequest.md)"> <strong>NdisOidDoubleRequest</strong> </a>ルールことを確認します。</p>
<ul>
<li><p>ミニポート ドライバーが完了する必要があります、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>現在保留中です。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"><strong>NdisTimedDataHang</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatahang.md" data-raw-source="[&lt;strong&gt;NdisTimedDataHang&lt;/strong&gt;](ndis-ndistimeddatahang.md)"> <strong>NdisTimedDataHang</strong> </a> NDIS ミニポート ドライバーでのすべての保留中の送信要求を処理するルールを確認します<a href="https://msdn.microsoft.com/library/windows/hardware/ff568388" data-raw-source="[&lt;strong&gt;NET_BUFFER_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568388)"> <strong>NET_BUFFER_LIST</strong> </a>22 秒内の構造。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"><strong>NdisTimedDataSend</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimeddatasend.md" data-raw-source="[&lt;strong&gt;NdisTimedDataSend&lt;/strong&gt;](ndis-ndistimeddatasend.md)"> <strong>NdisTimedDataSend</strong> </a>規則検証する NDIS ドライバーを呼び出すと<a href="https://msdn.microsoft.com/library/windows/hardware/ff559440" data-raw-source="[&lt;em&gt;MiniportSendNetBufferLists&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559440)"> <em>MiniportSendNetBufferLists</em></a>、ミニポート ドライバー30 秒以内には、送信要求を完了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"><strong>NdisTimedOidComplete</strong></a></p></td>
<td align="left"><p><a href="ndis-ndistimedoidcomplete.md" data-raw-source="[&lt;strong&gt;NdisTimedOidComplete&lt;/strong&gt;](ndis-ndistimedoidcomplete.md)"> <strong>NdisTimedOidComplete</strong> </a>ルールでは、NDIS ミニポート ドライバーが 12 秒以内、OID 要求を完了することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"><strong>WlanAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanassociation.md" data-raw-source="[&lt;strong&gt;WlanAssociation&lt;/strong&gt;](ndis-wlanassociation.md)"> <strong>WlanAssociation</strong> </a>ミニポート ドライバーが正しくネイティブ 802.11 ワイヤレス LAN (WLAN) の関連付けのシーケンスを次の規則を確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"><strong>WlanConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlanconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanConnectionRoaming&lt;/strong&gt;](ndis-wlanconnectionroaming.md)"> <strong>WlanConnectionRoaming</strong> </a>ミニポート ドライバーは、誤って、ネイティブの 802.11 ワイヤレス LAN (WLAN) 接続とローミングの順序に従ったルールを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"><strong>WlanDisassociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlandisassociation.md" data-raw-source="[&lt;strong&gt;WlanDisassociation&lt;/strong&gt;](ndis-wlandisassociation.md)"> <strong>WlanDisassociation</strong> </a>ルールは、ミニポート ドライバー正しくネイティブ 802.11 ワイヤレス LAN (WLAN) 関連付けの解除のシーケンスに従うことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"><strong>WlanTimedAssociation</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedassociation.md" data-raw-source="[&lt;strong&gt;WlanTimedAssociation&lt;/strong&gt;](ndis-wlantimedassociation.md)"> <strong>WlanTimedAssociation</strong> </a>ルールでは、NDIS ミニポート ドライバーが 10 秒後にワイヤレス LAN (WLAN) の関連付け操作が完了したことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"><strong>WlanTimedConnectionRoaming</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectionroaming.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectionRoaming&lt;/strong&gt;](ndis-wlantimedconnectionroaming.md)"> <strong>WlanTimedConnectionRoaming</strong> </a>ルールでは、NDIS ミニポート ドライバーが 10 秒以内に、ワイヤレス LAN (WLAN) 接続/移動操作を完了するを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"><strong>WlanTimedConnectRequest</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedconnectrequest.md" data-raw-source="[&lt;strong&gt;WlanTimedConnectRequest&lt;/strong&gt;](ndis-wlantimedconnectrequest.md)"> <strong>WlanTimedConnectRequest</strong> </a> 10 秒以内、NDIS_STATUS_DOT11_CONNECTION_START、OID_DOT11_CONNECT_REQUEST が後に、ルールを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"><strong>WlanTimedScan</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedscan.md" data-raw-source="[&lt;strong&gt;WlanTimedScan&lt;/strong&gt;](ndis-wlantimedscan.md)"> <strong>WlanTimedScan</strong> </a>ルールは、15 秒以内に WLAN のスキャン操作が完了したことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"><strong>WlanTimedLinkQuality</strong></a></p></td>
<td align="left"><p><a href="ndis-wlantimedlinkquality.md" data-raw-source="[&lt;strong&gt;WlanTimedLinkQuality&lt;/strong&gt;](ndis-wlantimedlinkquality.md)"> <strong>WlanTimedLinkQuality</strong> </a> NDIS_STATUS_DOT11_LINK_QUALITY indication が成功した NDIS_STATUS_DOT11_ASSOCIATION_COMPLETION 後 15 秒間で行われた規則を指定します。</p></td>
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
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 検証</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

 

 






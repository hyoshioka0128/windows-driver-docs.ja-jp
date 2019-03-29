---
title: NDIS ネットワーク インターフェイスの NDIS OID へのマッピング
description: NDIS ネットワーク インターフェイスの NDIS OID へのマッピング
ms.assetid: 117f94fd-829d-4ad8-be25-a6a90a8d4c50
keywords:
- ネットワーク インターフェイスの NDIS WDK、マッピング
- WDK のネットワーク インターフェイス、マッピング
- Oid WDK ネットワーク、ネットワーク インターフェイス
- OID 要求 WDK ネットワーク
- プロキシ インターフェイス プロバイダー WDK ネットワーク
- NDIS プロキシ インターフェイス プロバイダー WDK
- ネットワークの NDIS インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da61c06f09580ab717d81dd18cf67708b10ab083
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578506"
---
# <a name="mapping-of-ndis-network-interfaces-to-ndis-oids"></a>NDIS ネットワーク インターフェイスの NDIS OID へのマッピング





NDIS に応答するには、インターフェイス オブジェクトを要求する NDIS インターフェイス プロバイダーは、基になるドライバーから取得し、インターフェイスを基になる情報を取得する OID 要求を発行することも、情報をキャッシュできます。

プロキシ インターフェイス プロバイダーは、NDIS は通常、ミニポート アダプターとフィルター モジュールに関する情報を受け取ることをキャッシュします。 NDIS プロキシ インターフェイスのプロバイダーは、必要に応じて、インターフェイスの要求に応答する場合に、キャッシュされた情報を使用します。 場合によっては、NDIS プロキシ インターフェイス プロバイダーはインターフェイスの情報を取得する Oid を発行します。 たとえば、プライマリ情報のソース インターフェイスの NDIS 5。*x*あり、以前のドライバーを OID 要求を使用します。 NDIS 6.0 のドライバーの追加のインターフェイスの情報源として、 [ **NDIS\_再起動\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)と[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造体。 Oid の情報の代替ソースの詳細については、各 OID のリファレンス ページを参照してください。

NDIS プロキシ インターフェイス プロバイダーには、ミニポート アダプターとフィルター モジュールの代わりには、いくつかインターフェイス情報も生成されます。 たとえば、NDIS はインターフェイスのエイリアスを生成します。 (*ifAlias*で RFC 2863) への応答、 *ifAlias*要求。 NDIS は、NDIS インターフェイス プロバイダーからこのような情報を取得する追加の Oid を定義します。 たとえば、 [OID\_GEN\_エイリアス](https://msdn.microsoft.com/library/windows/hardware/ff569438)、インターフェイス プロバイダーを指定することができます、 *ifAlias*オブジェクト。 このような Oid はインターフェイス プロバイダーに固有し、他の NDIS ドライバーから情報を取得に使用されません。

インターフェイスのプロバイダーに固有の Oid、だけでなくインターフェイス プロバイダーは、NDIS は、インターフェイスの情報の取得に使用できるその他の NDIS Oid をサポートする必要があります。 NDIS がプロバイダーに Oid をこれら発行し、プロバイダーを発行できますこれら Oid、必要に応じて、基になるインターフェイスから情報を収集します。

**注**  NDIS RFC 2863 に含まれない追加の統計情報を定義します。 Oid にすべてのインターフェイスの NDIS でサポートされている統計をマップするリストのメンバーを参照してください、 [ **NDIS\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565736)構造体。 このトピックの表は、NDIS 実装の仕様を関連付けるしようとしているリーダーの RFC 2863 仕様で定義されている統計情報のマッピングを定義します。

 

次の表は、管理情報ベース (MIB) NDIS 6.0 の Oid を NDIS を使用する NDIS 5 から情報を取得する Oid で定義されているオブジェクトからマッピングを示します。*x*と以前のドライバーです。 テーブルには、MIB オブジェクトとして定義されていない一部の追加のインターフェイス オブジェクトも含まれています。 内のメンバーにも対応しているインターフェイス オブジェクト、 [ **NDIS\_インターフェイス\_情報**](ndis-interface-information.md)構造に関連付けられている、 [OID\_GEN\_インターフェイス\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569589)OID。

**注**  、NDIS 6.0 の Oid の表に、アスタリスクでマークされている (\*) は、インターフェイスのプロバイダーに固有のプレフィックス。 その他の NDIS 6.0 の Oid は、プロバイダーのインターフェイスとその他の NDIS ドライバーに発行できます。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インターフェイス MIB の値</th>
<th align="left">NDIS 6.0 の Oid</th>
<th align="left">NDIS 5.x と以前の Oid</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ifAdminStatus</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569437" data-raw-source="[OID_GEN_ADMIN_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569437)">OID_GEN_ADMIN_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifAlias</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569438" data-raw-source="[OID_GEN_ALIAS](https://msdn.microsoft.com/library/windows/hardware/ff569438)">OID_GEN_ALIAS</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifCounterDiscontinuityTime</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569581" data-raw-source="[OID_GEN_DISCONTINUITY_TIME](https://msdn.microsoft.com/library/windows/hardware/ff569581)">OID_GEN_DISCONTINUITY_TIME</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569441" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569441)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_RCV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInMulticastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569613" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569613)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInOctets</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569443" data-raw-source="[OID_GEN_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569443)">OID_GEN_BYTES_RCV</a></p></td>
<td align="left"><p>NDIS は、これらの Oid を収集するから結果を追加、 <em>ifHCInOctets</em> NDIS 5 の値<em>。x</em>ドライバー。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569577" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569577)">OID_GEN_DIRECTED_BYTES_RCV</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569611" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569611)">OID_GEN_MULTICAST_BYTES_RCV</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569439" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569439)">OID_GEN_BROADCAST_BYTES_RCV</a></p>
<p>NDIS 6.0 インターフェイス プロバイダーでは、これらの Oid もサポートする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInUcastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569579" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569579)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569442" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569442)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_XMIT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutMulticastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569614" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569614)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutOctets</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569445" data-raw-source="[OID_GEN_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569445)">OID_GEN_BYTES_XMIT</a></p></td>
<td align="left"><p>NDIS は、これらの Oid を収集するから結果を追加、 <em>ifHCInOctets</em> NDIS 5 の値<em>。x</em>ドライバー。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569578" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569578)">OID_GEN_DIRECTED_BYTES_XMIT</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569612" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569612)">OID_GEN_MULTICAST_BYTES_XMIT</a>+</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569440" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569440)">OID_GEN_BROADCAST_BYTES_XMIT</a></p>
<p>NDIS 6.0 インターフェイス プロバイダーでは、これらの Oid もサポートする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutUCastPkts</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569580" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569580)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHighSpeed</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569594" data-raw-source="[OID_GEN_LINK_SPEED_EX](https://msdn.microsoft.com/library/windows/hardware/ff569594)">OID_GEN_LINK_SPEED_EX</a>、* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569655" data-raw-source="[OID_GEN_XMIT_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569655)">OID_GEN_XMIT_LINK_SPEED</a>、* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569630" data-raw-source="[OID_GEN_RCV_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569630)">OID_GEN_RCV_LINK_SPEED</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569593" data-raw-source="[OID_GEN_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569593)">OID_GEN_LINK_SPEED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifInDiscards</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569628" data-raw-source="[OID_GEN_RCV_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569628)">OID_GEN_RCV_DISCARDS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifInErrors</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569629" data-raw-source="[OID_GEN_RCV_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569629)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>OID_GEN_RCV_ERROR</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifLastChange</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569591" data-raw-source="[OID_GEN_LAST_CHANGE](https://msdn.microsoft.com/library/windows/hardware/ff569591)">OID_GEN_LAST_CHANGE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifMtu</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569598" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569598)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>OID_GEN_MAXIMUM_FRAME_SIZE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOperStatus</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569619" data-raw-source="[OID_GEN_OPERATIONAL_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569619)">OID_GEN_OPERATIONAL_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifOutDiscards</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569653" data-raw-source="[OID_GEN_XMIT_DISCARDS](https://msdn.microsoft.com/library/windows/hardware/ff569653)">OID_GEN_XMIT_DISCARDS</a></p></td>
<td align="left"><p>OID_GEN_XMIT_DISCARDS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOutErrors</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569654" data-raw-source="[OID_GEN_XMIT_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569654)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>OID_GEN_XMIT_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifPhysAddress</em></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569069" data-raw-source="[OID_802_3_CURRENT_ADDRESS](https://msdn.microsoft.com/library/windows/hardware/ff569069)">OID_802_3_CURRENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_CURRENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifPromiscuousMode</em></p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569625" data-raw-source="[OID_GEN_PROMISCUOUS_MODE](https://msdn.microsoft.com/library/windows/hardware/ff569625)">OID_GEN_PROMISCUOUS_MODE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>適用なし</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569074" data-raw-source="[OID_802_3_PERMANENT_ADDRESS](https://msdn.microsoft.com/library/windows/hardware/ff569074)">OID_802_3_PERMANENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_PERMANENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>適用なし</p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569589" data-raw-source="[OID_GEN_INTERFACE_INFO](https://msdn.microsoft.com/library/windows/hardware/ff569589)">OID_GEN_INTERFACE_INFO</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>適用なし</p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569605" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS_EX](https://msdn.microsoft.com/library/windows/hardware/ff569605)">OID_GEN_MEDIA_CONNECT_STATUS_EX</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>適用なし</p></td>
<td align="left"><p>* <a href="https://msdn.microsoft.com/library/windows/hardware/ff569606" data-raw-source="[OID_GEN_MEDIA_DUPLEX_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569606)">OID_GEN_MEDIA_DUPLEX_STATE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>適用なし</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569640" data-raw-source="[OID_GEN_STATISTICS](https://msdn.microsoft.com/library/windows/hardware/ff569640)">OID_GEN_STATISTICS</a></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 






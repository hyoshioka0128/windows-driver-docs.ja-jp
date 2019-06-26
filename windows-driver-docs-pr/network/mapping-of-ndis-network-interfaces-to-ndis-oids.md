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
ms.openlocfilehash: 3889228d9d5f13372f2443661bcccec210c0d977
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387294"
---
# <a name="mapping-of-ndis-network-interfaces-to-ndis-oids"></a>NDIS ネットワーク インターフェイスの NDIS OID へのマッピング





NDIS に応答するには、インターフェイス オブジェクトを要求する NDIS インターフェイス プロバイダーは、基になるドライバーから取得し、インターフェイスを基になる情報を取得する OID 要求を発行することも、情報をキャッシュできます。

プロキシ インターフェイス プロバイダーは、NDIS は通常、ミニポート アダプターとフィルター モジュールに関する情報を受け取ることをキャッシュします。 NDIS プロキシ インターフェイスのプロバイダーは、必要に応じて、インターフェイスの要求に応答する場合に、キャッシュされた情報を使用します。 場合によっては、NDIS プロキシ インターフェイス プロバイダーはインターフェイスの情報を取得する Oid を発行します。 たとえば、プライマリ情報のソース インターフェイスの NDIS 5。*x*あり、以前のドライバーを OID 要求を使用します。 NDIS 6.0 のドライバーの追加のインターフェイスの情報源として、 [ **NDIS\_再起動\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_restart_attributes)と[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体。 Oid の情報の代替ソースの詳細については、各 OID のリファレンス ページを参照してください。

NDIS プロキシ インターフェイス プロバイダーには、ミニポート アダプターとフィルター モジュールの代わりには、いくつかインターフェイス情報も生成されます。 たとえば、NDIS はインターフェイスのエイリアスを生成します。 (*ifAlias*で RFC 2863) への応答、 *ifAlias*要求。 NDIS は、NDIS インターフェイス プロバイダーからこのような情報を取得する追加の Oid を定義します。 たとえば、 [OID\_GEN\_エイリアス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias)、インターフェイス プロバイダーを指定することができます、 *ifAlias*オブジェクト。 このような Oid はインターフェイス プロバイダーに固有し、他の NDIS ドライバーから情報を取得に使用されません。

インターフェイスのプロバイダーに固有の Oid、だけでなくインターフェイス プロバイダーは、NDIS は、インターフェイスの情報の取得に使用できるその他の NDIS Oid をサポートする必要があります。 NDIS がプロバイダーに Oid をこれら発行し、プロバイダーを発行できますこれら Oid、必要に応じて、基になるインターフェイスから情報を収集します。

**注**  NDIS RFC 2863 に含まれない追加の統計情報を定義します。 Oid にすべてのインターフェイスの NDIS でサポートされている統計をマップするリストのメンバーを参照してください、 [ **NDIS\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)構造体。 このトピックの表は、NDIS 実装の仕様を関連付けるしようとしているリーダーの RFC 2863 仕様で定義されている統計情報のマッピングを定義します。

 

次の表は、管理情報ベース (MIB) NDIS 6.0 の Oid を NDIS を使用する NDIS 5 から情報を取得する Oid で定義されているオブジェクトからマッピングを示します。*x*と以前のドライバーです。 テーブルには、MIB オブジェクトとして定義されていない一部の追加のインターフェイス オブジェクトも含まれています。 内のメンバーにも対応しているインターフェイス オブジェクト、 [ **NDIS\_インターフェイス\_情報**](ndis-interface-information.md)構造に関連付けられている、 [OID\_GEN\_インターフェイス\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info)OID。

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
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-admin-status" data-raw-source="[OID_GEN_ADMIN_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-admin-status)">OID_GEN_ADMIN_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifAlias</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias" data-raw-source="[OID_GEN_ALIAS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias)">OID_GEN_ALIAS</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifCounterDiscontinuityTime</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-discontinuity-time" data-raw-source="[OID_GEN_DISCONTINUITY_TIME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-discontinuity-time)">OID_GEN_DISCONTINUITY_TIME</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_RCV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInMulticastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCInOctets</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-rcv" data-raw-source="[OID_GEN_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-rcv)">OID_GEN_BYTES_RCV</a></p></td>
<td align="left"><p>NDIS は、これらの Oid を収集するから結果を追加、 <em>ifHCInOctets</em> NDIS 5 の値<em>。x</em>ドライバー。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv)">OID_GEN_DIRECTED_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv)">OID_GEN_MULTICAST_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv)">OID_GEN_BROADCAST_BYTES_RCV</a></p>
<p>NDIS 6.0 インターフェイス プロバイダーでは、これらの Oid もサポートする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCInUcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_RCV</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutBroadcastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_BROADCAST_FRAMES_XMIT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutMulticastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_MULTICAST_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHCOutOctets</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-xmit" data-raw-source="[OID_GEN_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-bytes-xmit)">OID_GEN_BYTES_XMIT</a></p></td>
<td align="left"><p>NDIS は、これらの Oid を収集するから結果を追加、 <em>ifHCInOctets</em> NDIS 5 の値<em>。x</em>ドライバー。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit)">OID_GEN_DIRECTED_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit)">OID_GEN_MULTICAST_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit)">OID_GEN_BROADCAST_BYTES_XMIT</a></p>
<p>NDIS 6.0 インターフェイス プロバイダーでは、これらの Oid もサポートする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifHCOutUCastPkts</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>OID_GEN_DIRECTED_FRAMES_XMIT</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifHighSpeed</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed-ex" data-raw-source="[OID_GEN_LINK_SPEED_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed-ex)">OID_GEN_LINK_SPEED_EX</a>、* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-link-speed" data-raw-source="[OID_GEN_XMIT_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-link-speed)">OID_GEN_XMIT_LINK_SPEED</a>、* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-link-speed" data-raw-source="[OID_GEN_RCV_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-link-speed)">OID_GEN_RCV_LINK_SPEED</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed" data-raw-source="[OID_GEN_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)">OID_GEN_LINK_SPEED</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifInDiscards</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-discards" data-raw-source="[OID_GEN_RCV_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-discards)">OID_GEN_RCV_DISCARDS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifInErrors</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error" data-raw-source="[OID_GEN_RCV_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>OID_GEN_RCV_ERROR</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifLastChange</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-last-change" data-raw-source="[OID_GEN_LAST_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-last-change)">OID_GEN_LAST_CHANGE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifMtu</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>OID_GEN_MAXIMUM_FRAME_SIZE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOperStatus</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-operational-status" data-raw-source="[OID_GEN_OPERATIONAL_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-operational-status)">OID_GEN_OPERATIONAL_STATUS</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifOutDiscards</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-discards" data-raw-source="[OID_GEN_XMIT_DISCARDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-discards)">OID_GEN_XMIT_DISCARDS</a></p></td>
<td align="left"><p>OID_GEN_XMIT_DISCARDS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifOutErrors</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error" data-raw-source="[OID_GEN_XMIT_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>OID_GEN_XMIT_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ifPhysAddress</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address" data-raw-source="[OID_802_3_CURRENT_ADDRESS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-current-address)">OID_802_3_CURRENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_CURRENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ifPromiscuousMode</em></p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-promiscuous-mode" data-raw-source="[OID_GEN_PROMISCUOUS_MODE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-promiscuous-mode)">OID_GEN_PROMISCUOUS_MODE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>該当なし</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-permanent-address" data-raw-source="[OID_802_3_PERMANENT_ADDRESS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-permanent-address)">OID_802_3_PERMANENT_ADDRESS</a></p></td>
<td align="left"><p>OID_802_3_PERMANENT_ADDRESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>該当なし</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info" data-raw-source="[OID_GEN_INTERFACE_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info)">OID_GEN_INTERFACE_INFO</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>該当なし</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status-ex" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status-ex)">OID_GEN_MEDIA_CONNECT_STATUS_EX</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>該当なし</p></td>
<td align="left"><p>* <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-duplex-state" data-raw-source="[OID_GEN_MEDIA_DUPLEX_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-duplex-state)">OID_GEN_MEDIA_DUPLEX_STATE</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>該当なし</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics" data-raw-source="[OID_GEN_STATISTICS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-statistics)">OID_GEN_STATISTICS</a></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 






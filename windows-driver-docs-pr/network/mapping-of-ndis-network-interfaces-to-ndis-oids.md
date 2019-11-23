---
title: NDIS ネットワーク インターフェイスの NDIS OID へのマッピング
description: NDIS ネットワーク インターフェイスの NDIS OID へのマッピング
ms.assetid: 117f94fd-829d-4ad8-be25-a6a90a8d4c50
keywords:
- NDIS ネットワークインターフェイス WDK、マッピング
- ネットワークインターフェイス WDK、マッピング
- Oid WDK ネットワーク、ネットワークインターフェイス
- OID が WDK ネットワークを要求する
- プロキシインターフェイスプロバイダーの WDK ネットワーク
- NDIS プロキシインターフェイスプロバイダー WDK
- NDIS ネットワークインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aaebb5df2236a57f7adc4f45b5b742c391e6708
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844303"
---
# <a name="mapping-of-ndis-network-interfaces-to-ndis-oids"></a>NDIS ネットワーク インターフェイスの NDIS OID へのマッピング





Ndis インターフェイスオブジェクトの要求に応答するために、NDIS インターフェイスプロバイダーは、基になるドライバーから取得した情報をキャッシュできます。また、基になるインターフェイスに関する情報を取得するために OID 要求を発行することもできます。

一般に、プロキシインターフェイスプロバイダーは、ミニポートアダプターおよびフィルターモジュールに関する情報をキャッシュします。 NDIS プロキシインターフェイスプロバイダーは、必要に応じて、インターフェイス要求に応答するために、キャッシュされた情報を使用します。 場合によっては、NDIS プロキシインターフェイスプロバイダーが Oid を発行して、インターフェイスの情報を取得します。 たとえば、NDIS 5 のインターフェイス情報の主要なソースです。*x*以前のドライバーは OID 要求を通じて行われます。 NDIS 6.0 ドライバーでは、 [**ndis\_RESTART\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)や[**NDIS\_ミニポート\_アダプター\_一般的な\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の構造など、インターフェイス情報の追加のソースがあります。 Oid に含まれる情報の代替ソースの詳細については、各 OID のリファレンスページを参照してください。

また、NDIS プロキシインターフェイスプロバイダーは、ミニポートアダプターとフィルターモジュールの代わりに、いくつかのインターフェイス情報を生成します。 たとえば、NDIS は*ifalias*要求に応じて、インターフェイスエイリアス (RFC 2863 では*ifalias* ) を生成します。 Ndis は、このような情報を NDIS インターフェイスプロバイダーから取得するための追加の Oid を定義します。 たとえば、 [OID\_GEN\_ALIAS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-alias)を使用すると、インターフェイスプロバイダーは*ifalias*オブジェクトを指定できます。 このような Oid は、インターフェイスプロバイダーに固有であり、他の NDIS ドライバーから情報を取得するために使用されることはありません。

インターフェイスプロバイダーに固有の Oid に加えて、インターフェイスプロバイダーは、NDIS がインターフェイス情報を取得するために使用できる他の NDIS Oid をサポートする必要があります。 NDIS はこれらの Oid をプロバイダーに発行できます。プロバイダーは、必要に応じて、基になるインターフェイスから情報を収集するためにこれらの Oid を発行できます。

**  NDIS**では、RFC 2863 に含まれていない追加の統計情報が定義されています。 NDIS でサポートされているすべてのインターフェイス統計を Oid にマップする一覧については、 [**ndis\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)構造体のメンバーを参照してください。 このトピックの表では、仕様を NDIS 実装に関連付けようとしているリーダーの RFC 2863 仕様で定義されている統計のマッピングを定義します。

 

次の表は、管理情報ベース (MIB) で定義されているオブジェクトから ndis 6.0 Oid と、ndis が NDIS 5 から情報を取得するために使用する Oid へのマッピングを示しています。*x*以前のドライバー。 この表には、MIB オブジェクトとして定義されていない追加のインターフェイスオブジェクトも含まれています。 インターフェイスオブジェクトは、 [OID\_GEN\_インターフェイス\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info)oid に関連付けられている[**NDIS\_インターフェイス\_情報**](ndis-interface-information.md)構造体のメンバーにも対応します。

アスタリスク (\*) プレフィックスでマークされているテーブル内の NDIS 6.0 Oid は、インターフェイスプロバイダーに固有の  に**注意**してください。 他の NDIS 6.0 Oid は、インターフェイスプロバイダーおよびその他の NDIS ドライバーに発行できます。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インターフェイスの MIB 値</th>
<th align="left">NDIS 6.0 Oid</th>
<th align="left">NDIS 5.x とそれ以前の Oid</th>
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
<td align="left"><p>NDIS は、これらの Oid から結果を追加して、NDIS 5 からの<em>ifHCInOctets</em>値を収集します。<em>x</em>ドライバー:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv)">OID_GEN_DIRECTED_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv)">OID_GEN_MULTICAST_BYTES_RCV</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv)">OID_GEN_BROADCAST_BYTES_RCV</a></p>
<p>NDIS 6.0 インターフェイスプロバイダーは、これらの Oid もサポートする必要があります。</p></td>
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
<td align="left"><p>NDIS は、これらの Oid から結果を追加して、NDIS 5 からの<em>ifHCInOctets</em>値を収集します。<em>x</em>ドライバー:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit)">OID_GEN_DIRECTED_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit)">OID_GEN_MULTICAST_BYTES_XMIT</a>+</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit)">OID_GEN_BROADCAST_BYTES_XMIT</a></p>
<p>NDIS 6.0 インターフェイスプロバイダーは、これらの Oid もサポートする必要があります。</p></td>
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

 

 

 






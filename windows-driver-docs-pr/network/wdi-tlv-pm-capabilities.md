---
title: WDI_TLV_PM_CAPABILITIES (0x42)
description: WDI_TLV_PM_CAPABILITIES は、電源管理機能を含む TLV です。
ms.assetid: DE8A5333-BE2B-4CBB-8C75-45ABBE35A635
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_CAPABILITIES (0x42) ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 003e1201cbb576f60706971528dfcac212cc906a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845154"
---
# <a name="wdi_tlv_pm_capabilities-0x42"></a>WDI\_TLV\_PM\_機能 (0x42)


WDI\_TLV\_PM\_機能は、電源管理機能を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x42

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>電源管理のサポートされているフラグを指定します。
<p>有効なフラグは次のとおりです。</p>
<ul>
<li>NDIS_PM_WAKE_PACKET_INDICATION_SUPPORTED</li>
<li>NDIS_PM_SELECTIVE_SUSPEND_SUPPORTED (0x00000002)</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされている Wake on LAN パターンを指定します。
<p>有効なパターンは次のとおりです。</p>
<ul>
<li>NDIS_PM_WOL_BITMAP_PATTERN_SUPPORTED (0x00000001)</li>
<li>NDIS_PM_WOL_MAGIC_PACKET_SUPPORTED (0x00000002)</li>
<li>NDIS_PM_WOL_IPV4_TCP_SYN_SUPPORTED (0x00000004)</li>
<li>NDIS_PM_WOL_IPV6_TCP_SYN_SUPPORTED (0x00000008)</li>
<li>NDIS_PM_WOL_IPV4_DEST_ADDR_WILDCARD_SUPPORTED (0x00000200)</li>
<li>NDIS_PM_WOL_IPV6_DEST_ADDR_WILDCARD_SUPPORTED (0x00000800)</li>
<li>NDIS_PM_WOL_EAPOL_REQUEST_ID_MESSAGE_SUPPORTED (0x00010000)</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>Wake on LAN のパターンの合計数を指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>Wake on LAN の最大のパターンサイズを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>Wake on LAN の最大のパターンオフセットを指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>Wake on LAN の最大パケット保存バッファーを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされているプロトコルオフロードを指定します。
<p>有効なオフロードは次のとおりです。</p>
<ul>
<li>NDIS_PM_PROTOCOL_OFFLOAD_ARP_SUPPORTED (0x00000001)</li>
<li>NDIS_PM_PROTOCOL_OFFLOAD_NS_SUPPORTED (0x00000002)</li>
<li>NDIS_PM_PROTOCOL_OFFLOAD_80211_RSN_REKEY_SUPPORTED (0x00000080)</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>ARP オフロード IPv4 アドレスの数を指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>NS オフロード IPv6 アドレスの数を指定します。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>最小マジックパケットウェイクアップを指定します。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>最小のパターンのウェイクアップを指定します。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state" data-raw-source="[&lt;strong&gt;NDIS_DEVICE_POWER_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)"><strong>NDIS_DEVICE_POWER_STATE</strong></a></td>
<td>最小リンク変更ウェイクアップを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされているウェイクアップイベントを指定します。
<p>有効なイベントは次のとおりです。</p>
<ul>
<li>NDIS_PM_WAKE_ON_MEDIA_CONNECT_SUPPORTED (0x00000001)</li>
<li>NDIS_PM_WAKE_ON_MEDIA_DISCONNECT_SUPPORTED (0x00000002)</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>メディア固有のウェイクアップイベントを指定します。
<p>有効なイベントは次のとおりです。</p>
<ul>
<li>NDIS_WLAN_WAKE_ON_NLO_DISCOVERY_SUPPORTED (0x00000001)</li>
<li>NDIS_WLAN_WAKE_ON_AP_ASSOCIATION_LOST_SUPPORTED (0x00000002)</li>
<li>NDIS_WLAN_WAKE_ON_GTK_HANDSHAKE_ERROR_SUPPORTED (0x00000004)</li>
<li>NDIS_WLAN_WAKE_ON_4WAY_HANDSHAKE_REQUEST_SUPPORTED (0x00000008)</li>
</ul></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





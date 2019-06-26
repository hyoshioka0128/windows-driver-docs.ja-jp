---
title: 一般的な OID
description: 一般的な OID
ms.assetid: fcd0e7fe-d1ab-4ec3-9c47-0bfb0ce63572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464651d01dde6cd518d4f3204e29b837e03eaeb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356277"
---
# <a name="general-oids"></a>一般的な OID





次の表には、リモートの NDIS イーサネット デバイスの一般的な Oid が一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サポート</th>
<th align="left">OID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-list" data-raw-source="[OID_GEN_SUPPORTED_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-list)">OID_GEN_SUPPORTED_LIST</a></p></td>
<td align="left"><p>サポートされている Oid の一覧です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hardware-status" data-raw-source="[OID_GEN_HARDWARE_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hardware-status)">OID_GEN_HARDWARE_STATUS</a></p></td>
<td align="left"><p>ハードウェアの状態。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-supported" data-raw-source="[OID_GEN_MEDIA_SUPPORTED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-supported)">OID_GEN_MEDIA_SUPPORTED</a></p></td>
<td align="left"><p>サポートされるメディア タイプ (エンコード)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-in-use" data-raw-source="[OID_GEN_MEDIA_IN_USE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-in-use)">OID_GEN_MEDIA_IN_USE</a></p></td>
<td align="left"><p>メディアの種類 (エンコード) を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>最大フレーム サイズ (バイト単位)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed" data-raw-source="[OID_GEN_LINK_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)">OID_GEN_LINK_SPEED</a></p></td>
<td align="left"><p>100 bps の単位でのリンク速度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-block-size" data-raw-source="[OID_GEN_TRANSMIT_BLOCK_SIZE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-block-size)">OID_GEN_TRANSMIT_BLOCK_SIZE</a></p></td>
<td align="left"><p>記憶域を 1 つのパケットを NIC の送信バッファー領域を占有するバイト単位の最小量</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-block-size" data-raw-source="[OID_GEN_RECEIVE_BLOCK_SIZE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-block-size)">OID_GEN_RECEIVE_BLOCK_SIZE</a></p></td>
<td align="left"><p>NIC の受信バッファー領域内に 1 つのパケットが占めるをバイト単位でのストレージの量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-id" data-raw-source="[OID_GEN_VENDOR_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-id)">OID_GEN_VENDOR_ID</a></p></td>
<td align="left"><p>仕入先の NIC のコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-description" data-raw-source="[OID_GEN_VENDOR_DESCRIPTION](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-description)">OID_GEN_VENDOR_DESCRIPTION</a></p></td>
<td align="left"><p>ベンダーのネットワーク カードの説明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-driver-version" data-raw-source="[OID_GEN_VENDOR_DRIVER_VERSION](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-vendor-driver-version)">OID_GEN_VENDOR_DRIVER_VERSION</a></p></td>
<td align="left"><p>ドライバーのベンダーが割り当てたバージョン番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)">OID_GEN_CURRENT_PACKET_FILTER</a></p></td>
<td align="left"><p>現在のパケット フィルター (エンコード)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-total-size" data-raw-source="[OID_GEN_MAXIMUM_TOTAL_SIZE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-total-size)">OID_GEN_MAXIMUM_TOTAL_SIZE</a></p></td>
<td align="left"><p>合計パケットの最大の長さ (バイト単位)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rndis-config-parameter" data-raw-source="[OID_GEN_RNDIS_CONFIG_PARAMETER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rndis-config-parameter)">OID_GEN_RNDIS_CONFIG_PARAMETER</a></p></td>
<td align="left"><p>デバイス固有の構成のパラメーター (set のみ)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium)">OID_GEN_PHYSICAL_MEDIUM</a></p></td>
<td align="left"><p>基になる物理メディアについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status)">OID_GEN_MEDIA_CONNECT_STATUS</a></p></td>
<td align="left"><p>NIC のネットワーク接続の状態です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-mac-options" data-raw-source="[OID_GEN_MAC_OPTIONS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-mac-options)">OID_GEN_MAC_OPTIONS</a></p></td>
<td align="left"><p>NIC の省略可能なプロパティを指定するビットマスク サポートされる Nic でのみサポートする必要<a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562331(v=vs.85)" data-raw-source="[802.1p packet priority](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff562331(v=vs.85))">802.1 p のパケットの優先順位</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 






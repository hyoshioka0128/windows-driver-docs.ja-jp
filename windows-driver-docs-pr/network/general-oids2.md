---
title: 一般的な Oid
description: 一般的な Oid
ms.assetid: fcd0e7fe-d1ab-4ec3-9c47-0bfb0ce63572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48c5b2899cbc974ea0c90d65bf9c4b93ffcdad5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560355"
---
# <a name="general-oids"></a>一般的な Oid





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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569642" data-raw-source="[OID_GEN_SUPPORTED_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569642)">OID_GEN_SUPPORTED_LIST</a></p></td>
<td align="left"><p>サポートされている Oid の一覧です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569585" data-raw-source="[OID_GEN_HARDWARE_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569585)">OID_GEN_HARDWARE_STATUS</a></p></td>
<td align="left"><p>ハードウェアの状態。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569609" data-raw-source="[OID_GEN_MEDIA_SUPPORTED](https://msdn.microsoft.com/library/windows/hardware/ff569609)">OID_GEN_MEDIA_SUPPORTED</a></p></td>
<td align="left"><p>サポートされるメディア タイプ (エンコード)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569607" data-raw-source="[OID_GEN_MEDIA_IN_USE](https://msdn.microsoft.com/library/windows/hardware/ff569607)">OID_GEN_MEDIA_IN_USE</a></p></td>
<td align="left"><p>メディアの種類 (エンコード) を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569598" data-raw-source="[OID_GEN_MAXIMUM_FRAME_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569598)">OID_GEN_MAXIMUM_FRAME_SIZE</a></p></td>
<td align="left"><p>最大フレーム サイズ (バイト単位)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569593" data-raw-source="[OID_GEN_LINK_SPEED](https://msdn.microsoft.com/library/windows/hardware/ff569593)">OID_GEN_LINK_SPEED</a></p></td>
<td align="left"><p>100 bps の単位でのリンク速度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569644" data-raw-source="[OID_GEN_TRANSMIT_BLOCK_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569644)">OID_GEN_TRANSMIT_BLOCK_SIZE</a></p></td>
<td align="left"><p>記憶域を 1 つのパケットを NIC の送信バッファー領域を占有するバイト単位の最小量</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569633" data-raw-source="[OID_GEN_RECEIVE_BLOCK_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569633)">OID_GEN_RECEIVE_BLOCK_SIZE</a></p></td>
<td align="left"><p>NIC の受信バッファー領域内に 1 つのパケットが占めるをバイト単位でのストレージの量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569651" data-raw-source="[OID_GEN_VENDOR_ID](https://msdn.microsoft.com/library/windows/hardware/ff569651)">OID_GEN_VENDOR_ID</a></p></td>
<td align="left"><p>仕入先の NIC のコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569649" data-raw-source="[OID_GEN_VENDOR_DESCRIPTION](https://msdn.microsoft.com/library/windows/hardware/ff569649)">OID_GEN_VENDOR_DESCRIPTION</a></p></td>
<td align="left"><p>ベンダーのネットワーク カードの説明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569650" data-raw-source="[OID_GEN_VENDOR_DRIVER_VERSION](https://msdn.microsoft.com/library/windows/hardware/ff569650)">OID_GEN_VENDOR_DRIVER_VERSION</a></p></td>
<td align="left"><p>ドライバーのベンダーが割り当てたバージョン番号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569575" data-raw-source="[OID_GEN_CURRENT_PACKET_FILTER](https://msdn.microsoft.com/library/windows/hardware/ff569575)">OID_GEN_CURRENT_PACKET_FILTER</a></p></td>
<td align="left"><p>現在のパケット フィルター (エンコード)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569601" data-raw-source="[OID_GEN_MAXIMUM_TOTAL_SIZE](https://msdn.microsoft.com/library/windows/hardware/ff569601)">OID_GEN_MAXIMUM_TOTAL_SIZE</a></p></td>
<td align="left"><p>合計パケットの最大の長さ (バイト単位)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569639" data-raw-source="[OID_GEN_RNDIS_CONFIG_PARAMETER](https://msdn.microsoft.com/library/windows/hardware/ff569639)">OID_GEN_RNDIS_CONFIG_PARAMETER</a></p></td>
<td align="left"><p>デバイス固有の構成のパラメーター (set のみ)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569621" data-raw-source="[OID_GEN_PHYSICAL_MEDIUM](https://msdn.microsoft.com/library/windows/hardware/ff569621)">OID_GEN_PHYSICAL_MEDIUM</a></p></td>
<td align="left"><p>基になる物理メディアについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必須</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569604" data-raw-source="[OID_GEN_MEDIA_CONNECT_STATUS](https://msdn.microsoft.com/library/windows/hardware/ff569604)">OID_GEN_MEDIA_CONNECT_STATUS</a></p></td>
<td align="left"><p>NIC のネットワーク接続の状態です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569597" data-raw-source="[OID_GEN_MAC_OPTIONS](https://msdn.microsoft.com/library/windows/hardware/ff569597)">OID_GEN_MAC_OPTIONS</a></p></td>
<td align="left"><p>NIC の省略可能なプロパティを指定するビットマスク サポートされる Nic でのみサポートする必要<a href="https://msdn.microsoft.com/library/windows/hardware/ff562331" data-raw-source="[802.1p packet priority](https://msdn.microsoft.com/library/windows/hardware/ff562331)">802.1 p のパケットの優先順位</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 






---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP は、IPv4 ARP プロトコルオフロードパラメーターを含む TLV です。
ms.assetid: 03894B22-3D4B-4262-893A-660FC88AA93D
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv4ARP ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 9717409d99dc1e86c36cf8b62304a2f5d4e5c788
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838013"
---
# <a name="wdi_tlv_pm_protocol_offload_ipv4arp"></a>WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP


WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv4ARP は、IPv4 ARP プロトコルオフロードパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x61

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | プロトコルオフロード ID を指定します。 オフロードプロトコルを識別する OS 提供の値です。 OS が追加要求を送信する前、またはそれ以降のドライバーへの要求を完了する前に、OS は ProtocolOffloadId をネットワークアダプターのプロトコルオフロード間で一意の値に設定します。                                                                   |
| UINT8\[4\]                                        | ARP 要求の発信元プロトコルアドレス (SPA) フィールドと一致させるオプションの IPv4 アドレスを指定します。 受信 ARP 要求にこの IPv4 アドレスと一致する SPA 値がある場合、ネットワークアダプターは、低電力状態のときに ARP 応答を送信します。 この値が0に設定されている場合、ネットワークアダプターは任意のリモート IPv4 アドレスからの ARP 要求に応答する必要があります。 |
| UINT8\[4\]                                        | ARP 応答を送信するときに、ネットワークアダプターが送信元プロトコルアドレス (SPA) フィールドに使用するホスト IPv4 アドレスを指定します。                                                                                                                                                                                                                                            |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ネットワークアダプターが生成する ARP 応答パケットの送信元ハードウェアアドレス (SHA) フィールドに使用する MAC アドレスを指定します。 ただし、MAC ヘッダーでは、ネットワークアダプターの現在の MAC アドレスをソースアドレスとして使用する必要があります。                                                                                                          |

 

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

 

 





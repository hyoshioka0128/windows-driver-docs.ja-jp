---
title: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS
description: WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS は、IPv6 NS プロトコルオフロードパラメーターを含む TLV です。
ms.assetid: 0385449B-82C6-44B4-BBD3-A708ADE54AC4
ms.date: 07/18/2017
keywords:
- WDI_TLV_PM_PROTOCOL_OFFLOAD_IPv6NS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 31985e9d5806147395d08a4aaf29c37f1ae9985d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838012"
---
# <a name="wdi_tlv_pm_protocol_offload_ipv6ns"></a>WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS


WDI\_TLV\_PM\_プロトコル\_オフロード\_IPv6NS は、IPv6 NS プロトコルオフロードパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x62

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                            | プロトコルオフロード ID を指定します。 オフロードプロトコルを識別する OS 提供の値です。 OS が追加要求を送信する前、またはそれ以降のドライバーへの要求を完了する前に、OS は ProtocolOffloadId をネットワークアダプターのプロトコルオフロード間で一意の値に設定します。                                                                                                    |
| UINT8\[16\]                                       | NS メッセージの IPv6 ヘッダーの [送信元アドレス] フィールドと照合する IPv6 アドレス (省略可能) を指定します。 受信した NS メッセージにこの IPv6 アドレスに一致する発信元アドレスの値がある場合、ネットワークアダプターは、そのメッセージが低電力状態のときに近隣通知 (NA) メッセージを送信します。 この値が0に設定されている場合、ネットワークアダプターは任意のリモート IPv6 アドレスからの NS メッセージに応答する必要があります。 |
| UINT8\[16\]                                       | 要請ノードの IPv6 アドレスを指定します。                                                                                                                                                                                                                                                                                                                                                                     |
| UINT8\[16\]                                       | 受信 NS メッセージのターゲットアドレスフィールドに一致する1つまたは2つの IPv6 アドレスを指定します。 アドレスが1つしかない場合、そのアドレスはターゲットアドレス1に格納され、ターゲットアドレス2には0が設定されます。 これらのアドレスのいずれかが受信 NS メッセージの [ターゲットアドレス] フィールドと一致する場合、ネットワークアダプターは応答で NA メッセージを送信します。                                               |
| UINT8\[16\]                                       | ターゲットアドレス1の説明を参照してください。                                                                                                                                                                                                                                                                                                                                                                           |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ネットワークアダプターが生成する NA メッセージのターゲットリンク層アドレス (TLLA) フィールドに使用する MAC アドレスを指定します。 ただし、MAC ヘッダーでは、ネットワークアダプターの現在の MAC アドレスをソースアドレスとして使用する必要があります。                                                                                                                                                 |

 

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

 

 





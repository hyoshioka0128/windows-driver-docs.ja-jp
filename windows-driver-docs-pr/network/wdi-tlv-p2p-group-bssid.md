---
title: WDI_TLV_P2P_GROUP_BSSID
description: WDI_TLV_P2P_GROUP_BSSID は、ローカル Wi-fi ダイレクト移動用のグループ BSSID を含む TLV です。
ms.assetid: C9BC2209-DF72-4775-A3B5-EC37D404CFED
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GROUP_BSSID ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 453977ebc508f75b4db4db7db7c22660091b521e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840441"
---
# <a name="wdi_tlv_p2p_group_bssid"></a>WDI\_TLV\_P2P\_グループ\_BSSID


WDI\_TLV\_P2P\_グループ\_BSSID は、ローカル Wi-fi ダイレクト移動用のグループ BSSID を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x73

## <a name="length"></a>長さ


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                          |
|---------------------------------------------------|------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ローカル Wi-fi ダイレクト移動用の "BSSID" グループを指定します。 |

 

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

 

 





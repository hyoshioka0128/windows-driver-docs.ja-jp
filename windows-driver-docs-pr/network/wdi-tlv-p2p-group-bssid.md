---
title: WDI_TLV_P2P_GROUP_BSSID
description: WDI_TLV_P2P_GROUP_BSSID では、ローカル Wi-Fi Direct GO 用のグループ BSSID を含む TLV です。
ms.assetid: C9BC2209-DF72-4775-A3B5-EC37D404CFED
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_GROUP_BSSID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 845a106737fb3ec322b9365ee2b5226e98437f82
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374674"
---
# <a name="wditlvp2pgroupbssid"></a>WDI\_TLV\_P2P\_グループ\_BSSID


WDI\_TLV\_P2P\_グループ\_BSSID はローカル Wi-Fi Direct GO 用のグループ BSSID を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x73

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体。

## <a name="values"></a>値


| 型                                              | 説明                                          |
|---------------------------------------------------|------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ローカル Wi-Fi Direct GO 用グループ BSSID を指定します。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 





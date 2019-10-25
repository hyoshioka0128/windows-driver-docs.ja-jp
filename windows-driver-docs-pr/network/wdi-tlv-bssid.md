---
title: WDI_TLV_BSSID
description: WDI_TLV_BSSID は、BSS の BSSID を含む TLV です。
ms.assetid: 0B3AB317-D1E7-4E61-9F6E-C3134B5A3984
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSSID ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e5da548315e36b9892e44f3870cd214721d5ed5d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844511"
---
# <a name="wdi_tlv_bssid"></a>WDI\_TLV\_BSSID


WDI\_TLV\_BSSID は、BSS の BSSID を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x2

## <a name="length"></a>長さ


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                 |
|---------------------------------------------------|---------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | BSSID を指定する Wi-fi MAC アドレス。 |

 

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

 

 





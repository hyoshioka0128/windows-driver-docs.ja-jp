---
title: WDI_TLV_BSSID
description: WDI_TLV_BSSID は、BSS の BSSID を含む TLV です。
ms.assetid: 0B3AB317-D1E7-4E61-9F6E-C3134B5A3984
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSSID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bdf3b31c431d147509c6c53047e6b71ef42fea08
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358595"
---
# <a name="wditlvbssid"></a>WDI\_TLV\_BSSID


WDI\_TLV\_BSSID BSS の BSSID を含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x2

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体。

## <a name="values"></a>値


| 型                                              | 説明                                 |
|---------------------------------------------------|---------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | BSSID を指定する Wi-fi MAC アドレスを指定します。 |

 

<a name="requirements"></a>必要条件
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

 

 





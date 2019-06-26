---
title: WDI_TLV_PEER_MAC_ADDRESS
description: WDI_TLV_PEER_MAC_ADDRESS では、ピアの MAC アドレスを含む TLV です。
ms.assetid: A936BAA6-96AD-4187-9933-FA02CCFED2AE
ms.date: 07/18/2017
keywords:
- WDI_TLV_PEER_MAC_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c3770c7fe9c673829a73a020873630876b6723d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385069"
---
# <a name="wditlvpeermacaddress"></a>WDI\_TLV\_ピア\_MAC\_アドレス


WDI\_TLV\_ピア\_MAC\_アドレスは、ピアの MAC アドレスを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x4C

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体。

## <a name="values"></a>値


| 型                                              | 説明                                  |
|---------------------------------------------------|----------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ピアの Wi-fi MAC アドレスを指定します。 |

 

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

 

 





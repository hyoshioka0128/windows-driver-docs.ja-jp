---
title: WDI_TLV_P2P_DEVICE_ADDRESS
description: WDI_TLV_P2P_DEVICE_ADDRESS では、グループの所有者のデバイスのアドレスを含む TLV です。
ms.assetid: EAC1972E-3D9B-4248-BAC3-3C2EB15D6817
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 855a06423dfddfe8333071c9a8edeb878197e3d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355098"
---
# <a name="wditlvp2pdeviceaddress"></a>WDI\_TLV\_P2P\_デバイス\_アドレス


WDI\_TLV\_P2P\_デバイス\_アドレスは、グループの所有者のデバイスのアドレスを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x91

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体。

## <a name="values"></a>値


| 型                                              | 説明                            |
|---------------------------------------------------|----------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | グループの所有者のデバイスのアドレス。 |

 

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

 

 





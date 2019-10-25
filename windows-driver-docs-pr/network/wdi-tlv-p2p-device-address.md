---
title: WDI_TLV_P2P_DEVICE_ADDRESS
description: WDI_TLV_P2P_DEVICE_ADDRESS は、グループ所有者のデバイスアドレスを含む TLV です。
ms.assetid: EAC1972E-3D9B-4248-BAC3-3C2EB15D6817
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_ADDRESS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 245e356deda7f838388ebee95d92eb4857bec9db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840453"
---
# <a name="wdi_tlv_p2p_device_address"></a>WDI\_TLV\_P2P\_デバイス\_アドレス


WDI\_TLV\_P2P\_デバイス\_アドレスは、グループ所有者のデバイスアドレスを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x91

## <a name="length"></a>Length


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造のサイズ (バイト単位)。

## <a name="values"></a>値


| 種類                                              | 説明                            |
|---------------------------------------------------|----------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | グループ所有者のデバイスアドレス。 |

 

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最低限のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小サーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





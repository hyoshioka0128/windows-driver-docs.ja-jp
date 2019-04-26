---
title: WDI_TLV_P2P_DEVICE_ADDRESS
description: WDI_TLV_P2P_DEVICE_ADDRESS では、グループの所有者のデバイスのアドレスを含む TLV です。
ms.assetid: EAC1972E-3D9B-4248-BAC3-3C2EB15D6817
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 99efe33e2d584128a8ff86091b6413553a91bee1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349340"
---
# <a name="wditlvp2pdeviceaddress"></a>WDI\_TLV\_P2P\_デバイス\_アドレス


WDI\_TLV\_P2P\_デバイス\_アドレスは、グループの所有者のデバイスのアドレスを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x91

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。

## <a name="values"></a>値


| 型                                              | 説明                            |
|---------------------------------------------------|----------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | グループの所有者のデバイスのアドレス。 |

 

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

 

 





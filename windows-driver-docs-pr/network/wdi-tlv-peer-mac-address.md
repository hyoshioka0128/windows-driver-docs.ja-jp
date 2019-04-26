---
title: WDI_TLV_PEER_MAC_ADDRESS
description: WDI_TLV_PEER_MAC_ADDRESS では、ピアの MAC アドレスを含む TLV です。
ms.assetid: A936BAA6-96AD-4187-9933-FA02CCFED2AE
ms.date: 07/18/2017
keywords:
- WDI_TLV_PEER_MAC_ADDRESS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 88fd71e809e182cefe1f1f6b0cf2400de6d44905
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349334"
---
# <a name="wditlvpeermacaddress"></a>WDI\_TLV\_ピア\_MAC\_アドレス


WDI\_TLV\_ピア\_MAC\_アドレスは、ピアの MAC アドレスを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x4C

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。

## <a name="values"></a>値


| 型                                              | 説明                                  |
|---------------------------------------------------|----------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | ピアの Wi-fi MAC アドレスを指定します。 |

 

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

 

 





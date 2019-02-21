---
title: WDI_TLV_BSSID
description: WDI_TLV_BSSID は、BSS の BSSID を含む TLV です。
ms.assetid: 0B3AB317-D1E7-4E61-9F6E-C3134B5A3984
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSSID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2bfdbf9fd0f9640f90383ae24b43818aa6f8edc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527774"
---
# <a name="wditlvbssid"></a>WDI\_TLV\_BSSID


WDI\_TLV\_BSSID BSS の BSSID を含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x2

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。

## <a name="values"></a>値


| 種類                                              | 説明                                 |
|---------------------------------------------------|---------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | BSSID を指定する Wi-fi MAC アドレスを指定します。 |

 

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

 

 





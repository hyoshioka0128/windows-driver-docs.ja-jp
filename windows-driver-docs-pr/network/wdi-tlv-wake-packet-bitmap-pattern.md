---
title: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN
description: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN では、wake on LAN のパターンを含む TLV です。
ms.assetid: 5BE0F668-A3B4-4ECF-B963-EC4DD1B1A8AE
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_BITMAP_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2d6f66c1bcaaf245f63a11b83da3c7d4a59d2403
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376355"
---
# <a name="wditlvwakepacketbitmappattern"></a>WDI\_TLV\_WAKE\_パケット\_ビットマップ\_パターン


WDI\_TLV\_WAKE\_パケット\_ビットマップ\_パターンは、wake on LAN のパターンを含む TLV します。

## <a name="tlv-type"></a>TLV 型


データ 0x5B

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------|
| [**WDI\_TLV\_WAKE\_パケット\_ビットマップ\_パターン\_ID**](wdi-tlv-wake-packet-bitmap-pattern-id.md) |                                |          | Wake on LAN のパターンの ID を指定します                                        |
| [**WDI\_TLV\_BITMAP\_PATTERN**](wdi-tlv-bitmap-pattern.md)                                  |                                |          | Wake on LAN のパターンを指定します。                                           |
| [**WDI\_TLV\_ビットマップ\_パターン\_マスク**](wdi-tlv-bitmap-pattern-mask.md)                       |                                |          | Wake on LAN のパターンのマスクを指定します。 長さが (PatternLength + 7)/8 です。 |

 

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

 

 





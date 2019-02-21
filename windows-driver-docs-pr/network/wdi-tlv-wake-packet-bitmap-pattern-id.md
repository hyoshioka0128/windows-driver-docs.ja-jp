---
title: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID
description: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID wake on LAN のパターンを含む TLV は ID です。
ms.assetid: 78807D91-189B-4E66-B3DC-500E9A59AEF2
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 39a2a8f54951c638b5f121110379580416418d07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552663"
---
# <a name="wditlvwakepacketbitmappatternid"></a>WDI\_TLV\_WAKE\_パケット\_ビットマップ\_パターン\_ID


WDI\_TLV\_WAKE\_パケット\_ビットマップ\_パターン\_ID は、wake on LAN のパターンの ID を含む TLV

パターンの ID は、wake on LAN のパターンを識別し、wake on LAN のパターンが、ネットワーク アダプター間で一意である値に設定されている OS で提供される値です。 OS の追加を基になるドライバーに送信または上にあるドライバーに要求を完了する前に、パターンの ID が設定されます。

## <a name="tlv-type"></a>TLV 型


0xE3

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 種類   | 説明                 |
|--------|-----------------------------|
| UINT32 | Wake on LAN のパターンの id。 |

 

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

## <a name="see-also"></a>関連項目


[OID\_WDI\_設定\_追加\_WOL\_パターン](https://msdn.microsoft.com/library/windows/hardware/dn925858)

 

 





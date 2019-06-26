---
title: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE
description: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE は、OID_WDI_SET_REMOVE_WOL_PATTERN で ID を削除するパターン ウェイク アップ パケットを含む TLV です。
ms.assetid: 69C87D35-AE6B-4F69-B099-A55B65EDAC58
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_PATTERN_REMOVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f6bb3c9578e9396d9ea8b07925bf3eb77dc7fd28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357103"
---
# <a name="wditlvwakepacketpatternremove"></a>WDI\_TLV\_WAKE\_パケット\_パターン\_削除


WDI\_TLV\_WAKE\_パケット\_パターン\_削除を削除するには、ウェイク アップ パケット パターン ID を含む TLV [OID\_WDI\_セット\_削除\_WOL\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-remove-wol-pattern)します。

## <a name="tlv-type"></a>TLV 型


0x6B

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                           |
|--------|---------------------------------------|
| UINT32 | ウェイク アップ パケットのパターンの ID を指定します |

 

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

 

 





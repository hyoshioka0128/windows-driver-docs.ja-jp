---
title: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE
description: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE は、OID_WDI_SET_REMOVE_WOL_PATTERN で ID を削除するパターン ウェイク アップ パケットを含む TLV です。
ms.assetid: 69C87D35-AE6B-4F69-B099-A55B65EDAC58
ms.date: 07/18/2017
keywords:
- WDI_TLV_WAKE_PACKET_PATTERN_REMOVE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 650254b6a9f35d2d9ff75e7392a4c8fefc200813
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382132"
---
# <a name="wditlvwakepacketpatternremove"></a>WDI\_TLV\_WAKE\_パケット\_パターン\_削除


WDI\_TLV\_WAKE\_パケット\_パターン\_削除を削除するには、ウェイク アップ パケット パターン ID を含む TLV [OID\_WDI\_セット\_削除\_WOL\_パターン](https://msdn.microsoft.com/library/windows/hardware/dn925944)します。

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

 

 





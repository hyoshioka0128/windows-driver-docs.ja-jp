---
title: WDI_TLV_SSID
description: WDI_TLV_SSID では、SSID を含む TLV です。
ms.assetid: 31391E25-B507-4652-9D70-9DA0D6245CA8
ms.date: 07/18/2017
keywords:
- WDI_TLV_SSID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 12ea12a875c7ffa359dd0da4a21ea88128caad89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560983"
---
# <a name="wditlvssid"></a>WDI\_TLV\_SSID


WDI\_TLV\_SSID は、SSID を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x3B

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 0 の配列の長さが許可されます。

## <a name="values"></a>値


| 種類      | 説明                                        |
|-----------|----------------------------------------------------|
| UINT8\[\] | SSID を指定する UINT8 要素の配列。 |

 

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

 

 





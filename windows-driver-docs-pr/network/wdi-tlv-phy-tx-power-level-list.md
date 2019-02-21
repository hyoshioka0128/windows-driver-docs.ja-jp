---
title: WDI_TLV_PHY_TX_POWER_LEVEL_LIST
description: WDI_TLV_PHY_TX_POWER_LEVEL_LIST では、電源のレベルの一覧を含む TLV です。
ms.assetid: DDBF9BBA-9700-4FD2-9521-6D0970E99893
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_TX_POWER_LEVEL_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8fedee8a5cea5c5ae2fc0473516e9d658784744f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537943"
---
# <a name="wditlvphytxpowerlevellist"></a>WDI\_TLV\_PHY\_TX\_POWER\_レベル\_一覧


WDI\_TLV\_PHY\_TX\_POWER\_レベル\_リストは、電源のレベルの一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x1C

## <a name="length"></a>長さ


Uint32 型の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類       | 説明                                              |
|------------|----------------------------------------------------------|
| UINT32\[\] | 電源のレベルを指定する UINT32 要素の配列。 |

 

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

 

 





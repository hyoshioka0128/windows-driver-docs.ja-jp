---
title: WDI_TLV_BITMAP_PATTERN
description: WDI_TLV_BITMAP_PATTERN では、パターンのバイト配列を含む TLV です。
ms.assetid: 44A18754-3D04-4B62-B8C2-861A47129F08
ms.date: 07/18/2017
keywords:
- WDI_TLV_BITMAP_PATTERN ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 065bc7c806ea6b5b5bfc0374d019fb134c8554b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558922"
---
# <a name="wditlvbitmappattern"></a>WDI\_TLV\_ビットマップ\_パターン


WDI\_TLV\_ビットマップ\_パターンは、パターンのバイト配列を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x68

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| UINT8\[\] | パターンのバイト配列を含む UINT8 要素の配列。 長さ = (パターンの長さ + 7)/8 です。 |

 

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

 

 





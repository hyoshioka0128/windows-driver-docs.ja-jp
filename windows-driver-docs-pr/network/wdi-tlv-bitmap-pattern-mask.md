---
title: WDI_TLV_BITMAP_PATTERN_MASK
description: WDI_TLV_BITMAP_PATTERN_MASK では、ビットマップのパターンのマスクを含む TLV です。
ms.assetid: 251B3496-04CE-419B-BE5E-C46265F50B7A
ms.date: 07/18/2017
keywords:
- WDI_TLV_BITMAP_PATTERN_MASK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 87b79c86464e4cead65e6a7267b9a5dc5e76ce9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374544"
---
# <a name="wditlvbitmappatternmask"></a>WDI\_TLV\_ビットマップ\_パターン\_マスク


WDI\_TLV\_ビットマップ\_パターン\_マスクはビットマップのパターンのマスクを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xE4

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                                                                                              |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | パターンのマスクのバイト配列を含む UINT8 要素の配列。 マスクはパターン バイトあたり 1 ビットが必要、(パターンの長さ + 7) のマスクの長さの等しいため/8 です。 |

 

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

 

 





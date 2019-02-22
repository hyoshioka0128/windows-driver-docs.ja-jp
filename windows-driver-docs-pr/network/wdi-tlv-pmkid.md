---
title: WDI_TLV_PMKID
description: WDI_TLV_PMKID は、PMKID 値を含む TLV です。
ms.assetid: 6873928B-7843-434F-AB80-6A7895D751A4
ms.date: 07/18/2017
keywords:
- WDI_TLV_PMKID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5f5f1ed0f4fe17721a91fa3dbd12ea27ae6863b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548727"
---
# <a name="wditlvpmkid"></a>WDI\_TLV\_PMKID


WDI\_TLV\_PMKID PMKID 値を含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x9F

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明            |
|-----------|------------------------|
| UINT8\[\] | 16 バイト PMKID 値。 |

 

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

 

 





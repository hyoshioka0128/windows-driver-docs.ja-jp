---
title: WDI_TLV_CIPHER_KEY_IHV_KEY
description: WDI_TLV_CIPHER_KEY_IHV_KEY では、IHV キーを格納した TLV です。
ms.assetid: 5814DEA6-038A-4CA6-8518-E8830BBA6B7F
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_IHV_KEY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 928712802624a90e8c1230216465a787b11d6014
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575003"
---
# <a name="wditlvcipherkeyihvkey"></a>WDI\_TLV\_暗号\_キー\_IHV\_キー


WDI\_TLV\_暗号\_キー\_IHV\_キーは IHV キーを格納した TLV します。

## <a name="tlv-type"></a>TLV 型


0x118

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                            |
|-----------|--------------------------------------------------------|
| UINT8\[\] | IHV キーを指定する UINT8 要素の配列。 |

 

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

 

 





---
title: WDI_TLV_FT_FTE
description: WDI_TLV_FT_FTE では、高速 Transition 要素を含む TLV です。
ms.assetid: E502508A-FB01-4F1E-9A68-40AA88894C61
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_FTE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c7fae0d2513243cb04316b9083f816f74ff32858
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532302"
---
# <a name="wditlvftfte"></a>WDI\_TLV\_FT\_FTE


WDI\_TLV\_FT\_FTE が高速 Transition 要素を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x10B

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                    |
|-----------|----------------------------------------------------------------|
| UINT8\[\] | 高速切り替え要素 R0KHID と SNonce が含まれています。 |

 

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

 

 





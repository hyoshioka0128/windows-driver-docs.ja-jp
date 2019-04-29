---
title: WDI_TLV_FT_AUTH_REQUEST
description: WDI_TLV_FT_AUTH_REQUEST では、高速切り替え認証要求のバイトの blob を含む TLV です。
ms.assetid: 4107314E-3C0A-4610-A4FB-BCBDBD1A8E65
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_AUTH_REQUEST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 50c62d072426cc7d2701ec455648b1abb5163d1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329864"
---
# <a name="wditlvftauthrequest"></a>WDI\_TLV\_FT\_AUTH\_要求


WDI\_TLV\_FT\_AUTH\_要求が高速切り替え認証要求のバイトの blob を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x119

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                    |
|-----------|------------------------------------------------------------------------------------------------|
| UINT8\[\] | 高速切り替え認証要求のバイトの blob を含む UINT8 要素の配列。 |

 

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

 

 





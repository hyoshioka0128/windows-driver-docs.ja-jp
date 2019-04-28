---
title: WDI_TLV_VENDOR_SPECIFIC_IE
description: WDI_TLV_VENDOR_SPECIFIC_IE では、ベンダー固有 IEs のリストを含む TLV です。
ms.assetid: 66995086-329A-49F1-B531-2AD2383473CF
ms.date: 07/18/2017
keywords:
- WDI_TLV_VENDOR_SPECIFIC_IE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3e6e3edc17f29e77ffd2592746fa2409b6ecca5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366608"
---
# <a name="wditlvvendorspecificie"></a>WDI\_TLV\_ベンダー\_特定\_IE


WDI\_TLV\_ベンダー\_特定\_IE ベンダー固有 IEs のリストを含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x5

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                        |
|-----------|--------------------------------------------------------------------|
| UINT8\[\] | ベンダー固有 IEs を示す UINT8 要素の配列。 |

 

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

 

 





---
title: WDI_TLV_BEACON_IES
description: WDI_TLV_BEACON_IES では、ビーコン IEs アソシエーションからを含む TLV です。
ms.assetid: A3E70310-2130-4248-B730-2DEF41C25993
ms.date: 07/18/2017
keywords:
- WDI_TLV_BEACON_IES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c2a5087f8adee98012114c79986a9ecaf7619080
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361888"
---
# <a name="wditlvbeaconies"></a>WDI\_TLV\_ビーコン\_IES


WDI\_TLV\_ビーコン\_IES ビーコン IEs アソシエーションからを含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x78

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                         |
|-----------|-------------------------------------|
| UINT8\[\] | アソシエーションからビーコン IEs します。 |

 

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

 

 





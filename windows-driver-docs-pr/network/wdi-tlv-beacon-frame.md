---
title: WDI_TLV_BEACON_FRAME
description: WDI_TLV_BEACON_FRAME では、ビーコン フレームを含む TLV です。
ms.assetid: 4022B721-B56E-482C-8F97-C4F7820CF6D1
ms.date: 07/18/2017
keywords:
- WDI_TLV_BEACON_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b0bccb86ff061a53a4b7389d73a533919c2c16ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361779"
---
# <a name="wditlvbeaconframe"></a>WDI\_TLV\_ビーコン\_フレーム


WDI\_TLV\_ビーコン\_フレームがビーコン フレームを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xa

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                 |
|-----------|-------------------------------------------------------------|
| UINT8\[\] | ビーコン フレームを指定する UINT8 要素の配列。 |

 

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

 

 





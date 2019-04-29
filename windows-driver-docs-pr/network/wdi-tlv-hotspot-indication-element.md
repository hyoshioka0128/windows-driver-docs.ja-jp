---
title: WDI_TLV_HOTSPOT_INDICATION_ELEMENT
description: WDI_TLV_HOTSPOT_INDICATION_ELEMENT では、アソシエーションの要求で使用されているホット スポットを示す値の要素が含まれる TLV です。
ms.assetid: 7A5B61B5-DFFF-4525-A6CD-2AC2822D8B86
ms.date: 07/18/2017
keywords:
- WDI_TLV_HOTSPOT_INDICATION_ELEMENT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 401838ba9bdc70c879b351199d946700047d29cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324280"
---
# <a name="wditlvhotspotindicationelement"></a>WDI\_TLV\_ホット スポット\_INDICATION\_要素


WDI\_TLV\_ホット スポット\_INDICATION\_要素は、アソシエーションの要求で使用されているホット スポットを示す値の要素が含まれる TLV します。

## <a name="tlv-type"></a>TLV 型


0x101

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                         |
|-----------|---------------------------------------------------------------------|
| UINT8\[\] | アソシエーションの要求で使用されているホット スポットを示す値の要素。 |

 

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

 

 





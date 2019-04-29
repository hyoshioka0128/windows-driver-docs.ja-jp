---
title: WDI_TLV_FT_MDE
description: WDI_TLV_FT_MDE は、BSS エントリの MDIE を含む TLV です。
ms.assetid: 2D075487-9B1E-4DEE-B3C3-3208C1CBAB64
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_MDE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5ad29a8f82b24f87822ef529fa3cea473b2f0122
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329874"
---
# <a name="wditlvftmde"></a>WDI\_TLV\_FT\_MDE


WDI\_TLV\_FT\_MDE BSS エントリの MDIE を含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x10D

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明              |
|-----------|--------------------------|
| UINT8\[\] | BSS エントリの MDIE します。 |

 

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

 

 





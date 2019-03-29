---
title: WDI_TLV_FT_RSNIE
description: WDI_TLV_FT_RSNIE では、高速の遷移 RSN IE バイトの blob を含む TLV です。
ms.assetid: 1EB22517-472C-461D-A32F-175E4281FFF0
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_RSNIE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d612a3f89611a7eb266efa4231de65042cca2a22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582437"
---
# <a name="wditlvftrsnie"></a>WDI\_TLV\_FT\_RSNIE


WDI\_TLV\_FT\_RSNIE が高速の遷移 RSN IE バイトの blob を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x10C

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                    |
|-----------|--------------------------------------------------------------------------------|
| UINT8\[\] | 高速の遷移 RSN IE バイトの blob を含む UINT8 要素の配列。 |

 

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

 

 





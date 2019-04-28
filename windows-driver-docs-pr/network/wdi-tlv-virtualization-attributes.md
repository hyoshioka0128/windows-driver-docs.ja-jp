---
title: WDI_TLV_VIRTUALIZATION_ATTRIBUTES
description: WDI_TLV_VIRTUALIZATION_ATTRIBUTES では、仮想化の属性を含む TLV です。
ms.assetid: BFB21903-2532-46FB-97E3-6AF254B6BB1E
ms.date: 07/18/2017
keywords:
- WDI_TLV_VIRTUALIZATION_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 01dcf187bd5ed6dcce89ebed930b23067486982f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377519"
---
# <a name="wditlvvirtualizationattributes"></a>WDI\_TLV\_VIRTUALIZATION\_属性


WDI\_TLV\_VIRTUALIZATION\_属性は、仮想化の属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x24

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                  | 許可されている複数の TLV インスタンス | 省略可能 | 説明                      |
|---------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------|
| [**WDI\_TLV\_VIRTUALIZATION\_機能**](wdi-tlv-virtualization-capabilities.md) |                                |          | 仮想化機能。 |

 

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

 

 





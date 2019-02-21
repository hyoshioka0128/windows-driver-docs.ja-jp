---
title: WDI_TLV_PHY_TYPE_LIST
description: WDI_TLV_PHY_TYPE_LIST は、PHY 型の配列を含む TLV です。
ms.assetid: 4066E4CE-D63E-4499-AE27-11F6BD57795D
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_TYPE_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ed175414be7b8d42f268e761aa3a016825ca2579
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549108"
---
# <a name="wditlvphytypelist"></a>WDI\_TLV\_PHY\_型\_一覧


WDI\_TLV\_PHY\_型\_リストが PHY 型の配列を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x19

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_PHY\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926105)値。 配列には、1 つ以上の値を含める必要があります。

## <a name="values"></a>値


| 種類                                            | 説明                  |
|-------------------------------------------------|------------------------------|
| [**WDI\_PHY\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926105)\[\] | PHY 型の値の配列。 |

 

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

 

 





---
title: WDI_TLV_PORT_ATTRIBUTES
description: WDI_TLV_PORT_ATTRIBUTES では、ポート属性を含む TLV です。
ms.assetid: F5A0BC8D-1B86-41C2-A530-860E15775695
ms.date: 07/18/2017
keywords:
- WDI_TLV_PORT_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 61552853ad51a798386a55e68f5b1ad087081e53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536379"
---
# <a name="wditlvportattributes"></a>WDI\_TLV\_ポート\_属性


WDI\_TLV\_ポート\_属性は、ポート属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x29

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                              | 説明                                         |
|---------------------------------------------------|-----------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | ポートに関連付けられている MAC アドレスを指定します。 |
| UINT16                                            | ポート番号を指定します。                          |

 

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

 

 





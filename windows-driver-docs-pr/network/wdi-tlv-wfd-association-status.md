---
title: WDI_TLV_WFD_ASSOCIATION_STATUS
description: WDI_TLV_WFD_ASSOCIATION_STATUS は、アソシエーションの要求が拒否された場合に設定される状態コードを含む TLV です。
ms.assetid: E97868FA-3F18-4EEF-B5EF-E2009381A16E
ms.date: 07/18/2017
keywords:
- WDI_TLV_WFD_ASSOCIATION_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 658ded9e9d7d508fc23c6b0b8c1398f5d85e765d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536518"
---
# <a name="wditlvwfdassociationstatus"></a>WDI\_TLV\_WFD\_アソシエーション\_状態


WDI\_TLV\_WFD\_アソシエーション\_状態は、アソシエーションの要求が拒否された場合に設定される状態コードを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x126

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                                   |
|-------|-------------------------------------------------------------------------------|
| UINT8 | DOT11\_WFD\_状態\_アソシエーションの要求が拒否されたときに設定するコードです。 |

 

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

 

 





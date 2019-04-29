---
title: WDI_TLV_OPERATION_MODE
description: WDI_TLV_OPERATION_MODE では、目的の操作モードを含む TLV です。
ms.assetid: CF5D9148-E50B-4F39-B37C-2495DE9A1488
ms.date: 07/18/2017
keywords:
- WDI_TLV_OPERATION_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c3f0cfdd77103cc9137eb5a83c68422634b8674b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385251"
---
# <a name="wditlvoperationmode"></a>WDI\_TLV\_操作\_モード


WDI\_TLV\_操作\_モードは、目的の操作モードを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x95

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| UINT32 | 定義されている、目的の操作モード[ **WDI\_操作\_モード**](https://msdn.microsoft.com/library/windows/hardware/dn926085)します。 |

 

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

 

 





---
title: WDI_TLV_HESSID
description: WDI_TLV_HESSID は、HESSIDs のリストを含む TLV です。
ms.assetid: 630A1824-7722-4B03-8073-EFC44E142400
ms.date: 07/18/2017
keywords:
- WDI_TLV_HESSID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ed53fe28a9e5975dbc38db0f150d942a49d0728d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548720"
---
# <a name="wditlvhessid"></a>WDI\_TLV\_HESSID


WDI\_TLV\_HESSID HESSIDs のリストを含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0xC8

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 種類                                                  | 説明        |
|-------------------------------------------------------|--------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)\[\] | HESSIDs の一覧。 |

 

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

 

 





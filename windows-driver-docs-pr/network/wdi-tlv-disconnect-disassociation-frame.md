---
title: WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME
description: WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME では、受信した関連付けの解除のフレームを含む TLV です。
ms.assetid: 0AE2A543-DA01-4CFB-853D-2511AB18F92C
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISCONNECT_DISASSOCIATION_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 481e698fb094ee5364f700417c9b2f20bf3be22a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582166"
---
# <a name="wditlvdisconnectdisassociationframe"></a>WDI\_TLV\_切断\_戻せません\_フレーム


WDI\_TLV\_切断\_戻せません\_フレームが受信した関連付けの解除のフレームを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x38

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                              |
|-----------|--------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 関連付けの解除を受信したフレームを含む UINT8 要素の配列。 これは、802.11 MAC ヘッダーには含まれません。 |

 

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

 

 





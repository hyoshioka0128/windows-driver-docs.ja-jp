---
title: WDI_TLV_CIPHER_KEY_CCMP_KEY
description: WDI_TLV_CIPHER_KEY_CCMP_KEY は、OID_WDI_SET_ADD_CIPHER_KEY の CCMP 暗号アルゴリズムのキー データを含む TLV です。
ms.assetid: A4754EAC-AA54-45CC-A7C5-B78A2757E012
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_CCMP_KEY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 38f85d2706ff35b030a83863e9e7afd8ddfded22
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387192"
---
# <a name="wditlvcipherkeyccmpkey"></a>WDI\_TLV\_暗号\_キー\_CCMP\_キー


WDI\_TLV\_暗号\_キー\_CCMP\_キーがの CCMP 暗号アルゴリズムのキー データを含む TLV [OID\_WDI\_設定\_の追加\_暗号\_キー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-add-cipher-keys)します。

## <a name="tlv-type"></a>TLV 型


0x50 です。

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                               |
|-----------|-------------------------------------------|
| UINT8\[\] | CCMP 暗号アルゴリズムのキー データを指定します。 |

 

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

 

 





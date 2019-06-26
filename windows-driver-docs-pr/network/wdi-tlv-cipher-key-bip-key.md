---
title: WDI_TLV_CIPHER_KEY_BIP_KEY
description: WDI_TLV_CIPHER_KEY_BIP_KEY は、OID_WDI_SET_ADD_CIPHER_KEYS の BIP 暗号アルゴリズムのキー データを含む TLV です。
ms.assetid: 99630BDF-9845-4E3D-AB18-5F5BAFCF7198
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_BIP_KEY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3c7b2e3c0366cf95c85f5f17f33606c7a9167ce4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387189"
---
# <a name="wditlvcipherkeybipkey"></a>WDI\_TLV\_暗号\_キー\_BIP\_キー


WDI\_TLV\_暗号\_キー\_BIP\_キーがの BIP 暗号アルゴリズムのキー データを含む TLV [OID\_WDI\_設定\_の追加\_暗号\_キー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-add-cipher-keys)します。

## <a name="tlv-type"></a>TLV 型


0x51

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                              |
|-----------|------------------------------------------|
| UINT8\[\] | BIP 暗号アルゴリズムのキー データを指定します。 |

 

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

 

 





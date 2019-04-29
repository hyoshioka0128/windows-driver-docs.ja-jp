---
title: WDI_TLV_CIPHER_KEY_BIP_KEY
description: WDI_TLV_CIPHER_KEY_BIP_KEY は、OID_WDI_SET_ADD_CIPHER_KEYS の BIP 暗号アルゴリズムのキー データを含む TLV です。
ms.assetid: 99630BDF-9845-4E3D-AB18-5F5BAFCF7198
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_BIP_KEY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 405b4c40ba8ccd2ebc37f9e8a27dc1cf1a55d4c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391018"
---
# <a name="wditlvcipherkeybipkey"></a>WDI\_TLV\_暗号\_キー\_BIP\_キー


WDI\_TLV\_暗号\_キー\_BIP\_キーがの BIP 暗号アルゴリズムのキー データを含む TLV [OID\_WDI\_設定\_の追加\_暗号\_キー](https://msdn.microsoft.com/library/windows/hardware/dn925855)します。

## <a name="tlv-type"></a>TLV 型


0x51

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                              |
|-----------|------------------------------------------|
| UINT8\[\] | BIP 暗号アルゴリズムのキー データを指定します。 |

 

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

 

 





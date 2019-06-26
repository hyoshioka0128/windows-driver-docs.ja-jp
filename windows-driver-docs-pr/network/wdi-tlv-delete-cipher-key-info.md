---
title: WDI_TLV_DELETE_CIPHER_KEY_INFO
description: WDI_TLV_DELETE_CIPHER_KEY_INFO は、OID_WDI_SET_DELETE_CIPHER_KEYS で削除する 1 つの暗号キーを識別するために情報を含む TLV です。
ms.assetid: 5AD84E05-9A25-4FE8-BDF4-CCBA89D09A3F
ms.date: 07/18/2017
keywords:
- WDI_TLV_DELETE_CIPHER_KEY_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b7751553c78fc2869dc5f49af846d6a6b8d98c27
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353616"
---
# <a name="wditlvdeletecipherkeyinfo"></a>WDI\_TLV\_削除\_暗号\_キー\_情報


WDI\_TLV\_削除\_暗号\_キー\_情報を使用して、削除する 1 つの暗号キーを識別するために情報を含む TLV [OID\_WDI\_設定\_削除\_暗号\_キー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-delete-cipher-keys)します。

## <a name="tlv-type"></a>TLV 型


0x53

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                      | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                |
|---------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ピア\_MAC\_アドレス**](wdi-tlv-peer-mac-address.md)          |                                | x        | ピアの MAC アドレスを指定します。 少なくとも 1 つの WDI\_TLV\_ピア\_MAC\_アドレスまたは WDI\_TLV\_暗号\_キー\_ID が存在する必要があります。 |
| [**WDI\_TLV\_暗号\_キー\_ID**](wdi-tlv-cipher-key-id.md)                |                                | x        | 暗号を指定しますキー id。 少なくとも 1 つの WDI\_TLV\_ピア\_MAC\_アドレスまたは WDI\_TLV\_暗号\_キー\_ID が存在する必要があります。    |
| [**WDI\_TLV\_暗号\_キー\_型\_情報**](wdi-tlv-cipher-key-type-info.md) |                                |          | 暗号キーの種類の情報を指定します。                                                                                 |

 

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

 

 





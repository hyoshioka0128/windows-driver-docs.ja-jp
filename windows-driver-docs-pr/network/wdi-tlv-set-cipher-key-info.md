---
title: WDI_TLV_SET_CIPHER_KEY_INFO
description: WDI_TLV_SET_CIPHER_KEY_INFO は、OID_WDI_SET_ADD_CIPHER_KEYS の暗号キー マッピングのキー情報を含む TLV です。
ms.assetid: 6352284A-73CD-4B15-A057-80D0C8518CD5
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_CIPHER_KEY_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b589762b6c8f098e5e2ff2b5b264e97d4baa490c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535427"
---
# <a name="wditlvsetcipherkeyinfo"></a>WDI\_TLV\_設定\_暗号\_キー\_情報


WDI\_TLV\_設定\_暗号\_キー\_情報は、の暗号キー マッピングのキー情報を含む TLV [OID\_WDI\_設定\_追加\_暗号\_キー](https://msdn.microsoft.com/library/windows/hardware/dn925855)します。

## <a name="tlv-type"></a>TLV 型


0x52

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                 | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                                                                                                                                                       |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_ピア\_MAC\_アドレス**](wdi-tlv-peer-mac-address.md)                                     |                                | X        | このキーが関連付けられているピアの MAC アドレスを指定します。 いない場合は、表示、これは、既定のキーを前提としています。 少なくとも 1 つのピアの MAC アドレスまたは暗号のキー ID が存在する必要があります。 このフィールドは WDI にキーの種類を設定するときに存在する必要があります\_暗号\_キー\_型\_PAIRWISE\_キー、WDI にキーの種類を設定するときに存在する場合がありますと\_暗号\_キー\_型\_グループ\_キー。 |
| [**WDI\_TLV\_暗号\_キー\_ID**](wdi-tlv-cipher-key-id.md)                                           |                                | X        | この暗号キーの ID を指定します。 少なくとも 1 つのピアの MAC アドレスまたは暗号キー ID が存在する必要があります。 このフィールドは、ペアワイズ キーの必要はありません。                                                                                                                                                                                                            |
| [**WDI\_TLV\_暗号\_キー\_型\_情報**](wdi-tlv-cipher-key-type-info.md)                            |                                |          | 暗号キーの種類の情報を指定します。                                                                                                                                                                                                                                                                                                                        |
| [**WDI\_TLV\_暗号\_キー\_受信\_シーケンス\_数**](wdi-tlv-cipher-key-receive-sequence-count.md) |                                | X        | パケット数 (PN)、再生の保護に使用される初期 48 ビット値を指定します。 これは、暗号アルゴリズムが WDI 場合は省略可能\_暗号\_ALGO\_WEP40、WDI\_暗号\_ALGO\_WEP104、または WDI\_暗号\_ALGO\_。WEP します。                                                                                                                                        |
| [**WDI\_TLV\_暗号\_キー\_CCMP\_キー**](wdi-tlv-cipher-key-ccmp-key.md)                              |                                | X        | CCMP 暗号アルゴリズムのキー データを指定します。 これは、暗号アルゴリズムが WDI 場合のみ\_暗号\_ALGO\_CCMP します。                                                                                                                                                                                                                                            |
| [**WDI\_TLV\_暗号\_キー\_TKIP\_情報**](wdi-tlv-cipher-key-tkip-info.md)                            |                                | X        | [Tkip] 情報を指定します。 これは、暗号アルゴリズムが WDI 場合のみ\_暗号\_ALGO\_[tkip] です。                                                                                                                                                                                                                                                          |
| [**WDI\_TLV\_暗号\_キー\_BIP\_キー**](wdi-tlv-cipher-key-bip-key.md)                                |                                | X        | BIP キーを指定します。 これは、暗号アルゴリズムが WDI 場合のみ\_暗号\_ALGO\_BIP します。                                                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_暗号\_キー\_WEP\_キー**](wdi-tlv-cipher-key-wep-key.md)                                |                                | X        | WEP キーを指定します。 これは、暗号アルゴリズムが WDI 場合のみ\_暗号\_ALGO\_WEP40、WDI\_暗号\_ALGO\_WEP104、または WDI\_暗号\_ALGO\_WEP します。                                                                                                                                                                                                            |
| [**WDI\_TLV\_暗号\_キー\_IHV\_キー**](wdi-tlv-cipher-key-ihv-key.md)                                |                                | X        | IHV 暗号キーを指定します。 これは場合にのみ存在[ **WDI\_TLV\_暗号\_キー\_型\_情報**](wdi-tlv-cipher-key-type-info.md)範囲 WDI に\_暗号\_ALGO\_IHV\_WDI に\_暗号\_ALGO\_IHV\_終了します。                                                                                                                                                     |

 

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

 

 





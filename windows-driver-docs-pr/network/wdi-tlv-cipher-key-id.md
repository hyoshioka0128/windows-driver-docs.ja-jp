---
title: WDI_TLV_CIPHER_KEY_ID
description: WDI_TLV_CIPHER_KEY_ID が暗号を含む TLV OID_WDI_SET_ADD_CIPHER_KEYS と OID_WDI_SET_DELETE_CIPHER_KEYS キー ID。
ms.assetid: 24076B2A-FAC2-4509-9F1C-7F2AF57883CF
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3d359e762aeca4351a855b151d3891a4eb9b60cc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387187"
---
# <a name="wditlvcipherkeyid"></a>WDI\_TLV\_暗号\_キー\_ID


WDI\_TLV\_暗号\_キー\_ID を含む、暗号 TLV は、キーの ID [OID\_WDI\_設定\_追加\_暗号\_キー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-add-cipher-keys)と[OID\_WDI\_設定\_削除\_暗号\_キー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-delete-cipher-keys)します。

## <a name="tlv-type"></a>TLV 型


0x4D

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                  |
|--------|------------------------------|
| UINT32 | 暗号を指定しますキー id。 |

 

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

 

 





---
title: WDI_TLV_CIPHER_KEY_TYPE_INFO
description: WDI_TLV_CIPHER_KEY_TYPE_INFO は、OID_WDI_SET_ADD_CIPHER_KEYS と OID_WDI_SET_DELETE_CIPHER_KEYS の暗号キーの種類の情報を含む TLV です。
ms.assetid: 1168D53D-A837-4E3F-8E31-FB86CF866BA3
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_TYPE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 95ed5ff3d67c4be4acd74f4acc830e6b21d110f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362822"
---
# <a name="wditlvcipherkeytypeinfo"></a>WDI\_TLV\_暗号\_キー\_型\_情報


WDI\_TLV\_暗号\_キー\_型\_情報は、暗号キーの種類の情報を含む TLV [OID\_WDI\_設定\_の追加\_暗号\_キー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-add-cipher-keys)と[OID\_WDI\_設定\_削除\_暗号\_キー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-delete-cipher-keys)します。

## <a name="tlv-type"></a>TLV 型


0x4E

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                 | 説明                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm)          | キーを使用する暗号アルゴリズムを指定します。                                                                                                                                                                                                                                               |
| [**WDI\_暗号\_キー\_方向**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_key_direction) | キーを使用するかどうかを指定のみを送信、受信のみ、またはその両方です。                                                                                                                                                                                                              |
| UINT8                                                                | ポートが、ローミングのキーを削除するかどうかを指定します。 この値が 0 に設定されている場合は、ポート、BSS ネットワークから切断または BSS ネットワークに接続するときに、キーを削除する必要があります。 この値が 1 に設定されている場合、明示的な削除またはリセット要求にキーを削除する必要があります。 |
| [**WDI\_暗号\_キー\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_key_type)           | パブリッシュされているキーの種類を指定します。                                                                                                                                                                                                                                                      |

 

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

 

 





---
title: WDI_TLV_CIPHER_KEY_TYPE_INFO
description: WDI_TLV_CIPHER_KEY_TYPE_INFO は、OID_WDI_SET_ADD_CIPHER_KEYS と OID_WDI_SET_DELETE_CIPHER_KEYS の暗号キーの種類の情報を含む TLV です。
ms.assetid: 1168D53D-A837-4E3F-8E31-FB86CF866BA3
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_TYPE_INFO ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f6fe3691a85a81ad8eaca6f111973f9aa20b0f5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843393"
---
# <a name="wdi_tlv_cipher_key_type_info"></a>WDI\_TLV\_暗号\_キー\_種類\_情報


WDI\_TLV\_暗号\_キー\_型\_情報は、 [oid\_WDI\_SET\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-add-cipher-keys)暗号キーの種類の情報を含む TLV であり\_暗号\_キーおよび OID を追加 @no__ [t_12_ WDI\_\_暗号\_キーを削除\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-delete-cipher-keys)します。

## <a name="tlv-type"></a>TLV 型


0x4E

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                 | 説明                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_暗号\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)          | キーを使用する暗号アルゴリズムを指定します。                                                                                                                                                                                                                                               |
| [**WDI\_暗号\_キー\_方向**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_direction) | キーを送信専用、受信のみ、またはその両方に使用するかどうかを指定します。                                                                                                                                                                                                              |
| UINT8                                                                | ポートでローミング時にキーを削除するかどうかを指定します。 この値が0に設定されている場合、ポートが BSS ネットワークから切断されたとき、または BSS ネットワークに接続するときに、キーを削除する必要があります。 この値が1に設定されている場合は、明示的な削除またはリセット要求でキーを削除する必要があります。 |
| [**WDI\_暗号\_キー\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_type)           | 発行されるキーの種類を指定します。                                                                                                                                                                                                                                                      |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





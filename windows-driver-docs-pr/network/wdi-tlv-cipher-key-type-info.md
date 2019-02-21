---
title: WDI_TLV_CIPHER_KEY_TYPE_INFO
description: WDI_TLV_CIPHER_KEY_TYPE_INFO は、OID_WDI_SET_ADD_CIPHER_KEYS と OID_WDI_SET_DELETE_CIPHER_KEYS の暗号キーの種類の情報を含む TLV です。
ms.assetid: 1168D53D-A837-4E3F-8E31-FB86CF866BA3
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_TYPE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6ed6349b7e68d5872ef1b03bdeaf692cfe2ca33c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553841"
---
# <a name="wditlvcipherkeytypeinfo"></a>WDI\_TLV\_暗号\_キー\_型\_情報


WDI\_TLV\_暗号\_キー\_型\_情報は、暗号キーの種類の情報を含む TLV [OID\_WDI\_設定\_の追加\_暗号\_キー](https://msdn.microsoft.com/library/windows/hardware/dn925855)と[OID\_WDI\_設定\_削除\_暗号\_キー](https://msdn.microsoft.com/library/windows/hardware/dn925929)します。

## <a name="tlv-type"></a>TLV 型


0x4E

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                                                 | 説明                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_暗号\_アルゴリズム**](https://msdn.microsoft.com/library/windows/hardware/dn897802)          | キーを使用する暗号アルゴリズムを指定します。                                                                                                                                                                                                                                               |
| [**WDI\_暗号\_キー\_方向**](https://msdn.microsoft.com/library/windows/hardware/dn897803) | キーを使用するかどうかを指定のみを送信、受信のみ、またはその両方です。                                                                                                                                                                                                              |
| UINT8                                                                | ポートが、ローミングのキーを削除するかどうかを指定します。 この値が 0 に設定されている場合は、ポート、BSS ネットワークから切断または BSS ネットワークに接続するときに、キーを削除する必要があります。 この値が 1 に設定されている場合、明示的な削除またはリセット要求にキーを削除する必要があります。 |
| [**WDI\_暗号\_キー\_型**](https://msdn.microsoft.com/library/windows/hardware/dn897806)           | パブリッシュされているキーの種類を指定します。                                                                                                                                                                                                                                                      |

 

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

 

 





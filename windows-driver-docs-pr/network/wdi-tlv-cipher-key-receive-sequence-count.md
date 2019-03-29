---
title: WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT
description: WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT では、受信シーケンス数を含む TLV です。
ms.assetid: 29AA9D90-834F-4043-B12A-87705EDC1DF0
ms.date: 07/18/2017
keywords:
- WDI_TLV_CIPHER_KEY_RECEIVE_SEQUENCE_COUNT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 076e34f0acff9e671bd3582ee58df8d269d96b99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579603"
---
# <a name="wditlvcipherkeyreceivesequencecount"></a>WDI\_TLV\_暗号\_キー\_受信\_シーケンス\_数


WDI\_TLV\_暗号\_キー\_受信\_シーケンス\_数が、受信シーケンス カウントを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x4F

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。

## <a name="values"></a>値


| 型       | 説明                                                                                    |
|------------|------------------------------------------------------------------------------------------------|
| UINT8\[6\] | パケット数 (PN)、再生の保護に使用される初期 48 ビット値を指定します。 |

 

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

 

 





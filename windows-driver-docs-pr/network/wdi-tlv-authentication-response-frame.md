---
title: WDI_TLV_AUTHENTICATION_RESPONSE_FRAME
description: WDI_TLV_ASSOCIATION_RESPONSE_FRAME では、認証の応答フレームを含む TLV です。
ms.assetid: 0BD8BDD9-7D51-413F-8740-FD49F71249B1
ms.date: 07/18/2017
keywords:
- WDI_TLV_AUTHENTICATION_RESPONSE_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d17dd3a3f39809a57d874ebe009ed3f09bd76edb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536969"
---
# <a name="wditlvauthenticationresponseframe"></a>WDI\_TLV\_認証\_応答\_フレーム


WDI\_TLV\_アソシエーション\_応答\_フレームは、認証応答のフレームを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x124

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | エラー コードを受信した認証の応答を含む UINT8 要素の配列。 これは、802.11 MAC ヘッダーには含まれません。 |

 

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

 

 





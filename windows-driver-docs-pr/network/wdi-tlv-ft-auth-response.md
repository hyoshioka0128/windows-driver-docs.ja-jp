---
title: WDI_TLV_FT_AUTH_RESPONSE
description: WDI_TLV_FT_AUTH_RESPONSE では、高速切り替え認証応答バイトの blob を含む TLV です。
ms.assetid: BF9B37B4-EC5D-46AA-B334-C1214310964B
ms.date: 07/18/2017
keywords:
- WDI_TLV_FT_AUTH_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a34954f5b82815ef62adeaf8009061fee1cfbb5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329732"
---
# <a name="wditlvftauthresponse"></a>WDI\_TLV\_FT\_AUTH\_応答


WDI\_TLV\_FT\_AUTH\_応答が高速切り替え認証応答バイトの blob を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x10E

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                     |
|-----------|-------------------------------------------------------------------------------------------------|
| UINT8\[\] | 高速切り替え認証応答バイトの blob を含む UINT8 要素の配列。 |

 

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

 

 





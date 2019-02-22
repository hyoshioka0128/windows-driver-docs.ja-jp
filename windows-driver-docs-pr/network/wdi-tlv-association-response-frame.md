---
title: WDI_TLV_ASSOCIATION_RESPONSE_FRAME
description: WDI_TLV_ASSOCIATION_RESPONSE_FRAME では、受信したアソシエーションの応答を含む TLV です。
ms.assetid: FA71F8CA-BA22-4EF2-8DF4-2A08C83A54A7
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESPONSE_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 63275012362764ae538d30a9cfab2d19ba281b82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529491"
---
# <a name="wditlvassociationresponseframe"></a>WDI\_TLV\_アソシエーション\_応答\_フレーム


WDI\_TLV\_アソシエーション\_応答\_フレームが受信したアソシエーションの応答を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x2F

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                                                                              |
|-----------|--------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 受信したアソシエーションの応答を含む UINT8 要素の配列。 これは、802.11 MAC ヘッダーには含まれません。 |

 

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

 

 





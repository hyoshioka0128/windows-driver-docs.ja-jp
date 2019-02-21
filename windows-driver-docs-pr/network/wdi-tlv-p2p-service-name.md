---
title: WDI_TLV_P2P_SERVICE_NAME
description: WDI_TLV_P2P_SERVICE_NAME では、サービスの名前を含む TLV です。
ms.assetid: 6394F781-BFE7-4009-8F5E-72D7C8CCF036
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_NAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: adaeec3ca664978df0c1e00677a75346e12389b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530962"
---
# <a name="wditlvp2pservicename"></a>WDI\_TLV\_P2P\_サービス\_名


WDI\_TLV\_P2P\_サービス\_名は、サービスの名前を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xec です。

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                         |
|-----------|-----------------------------------------------------|
| UINT8\[\] | Utf-8、最大 255 バイトでは、サービスの名前。 |

 

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

 

 





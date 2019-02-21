---
title: WDI_TLV_P2P_SERVICE_INFORMATION
description: WDI_TLV_P2P_SERVICE_INFORMATION では、Wi-Fi Direct サービスの情報を含む TLV です。
ms.assetid: C377FA31-1D78-4087-A600-18F10D9022B6
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_INFORMATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d5b182411c3c2ad30f29962b93df4431d2a799ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557922"
---
# <a name="wditlvp2pserviceinformation"></a>WDI\_TLV\_P2P\_サービス\_情報


WDI\_TLV\_P2P\_サービス\_情報は、Wi-Fi Direct サービスの情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xee

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                              |
|-----------|------------------------------------------|
| UINT8\[\] | サービスのサービス情報。 |

 

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

 

 





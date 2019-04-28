---
title: WDI_TLV_P2P_SERVICE_TYPE
description: WDI_TLV_P2P_SERVICE_TYPE では、サービスのサービスの種類を含む TLV です。
ms.assetid: D9C3F099-DED1-400E-9D3F-7AF6D2D286DF
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SERVICE_TYPE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4fd6f6ffbdeefe833d7c2c502b03e32019127601
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375616"
---
# <a name="wditlvp2pservicetype"></a>WDI\_TLV\_P2P\_サービス\_型


WDI\_TLV\_P2P\_サービス\_型は、サービスのサービスの種類を含む TLV します。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x129

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                    |
|-----------|----------------------------------------------------------------|
| UINT8\[\] | Utf-8、21 の最大バイト長で、サービスのサービスの種類。 |

 

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

 

 





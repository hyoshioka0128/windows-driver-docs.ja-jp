---
title: WDI_TLV_P2P_INSTANCE_NAME
description: WDI_TLV_P2P_INSTANCE_NAME では、サービスのインスタンス名を含む TLV です。
ms.assetid: 36CB51E2-D8CB-4C71-B2DB-77F4FDBB8B90
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INSTANCE_NAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4d26711f00edc3d1cf677d0a2c3b5b765295d29f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536607"
---
# <a name="wditlvp2pinstancename"></a>WDI\_TLV\_P2P\_インスタンス\_名


WDI\_TLV\_P2P\_インスタンス\_名は、サービスのインスタンス名を含む TLV します。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x12B

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                     |
|-----------|-----------------------------------------------------------------|
| UINT8\[\] | Utf-8、最大 63 バイト長で、サービスのインスタンスの名前。 |

 

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

 

 





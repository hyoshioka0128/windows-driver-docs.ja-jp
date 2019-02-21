---
title: WDI_TLV_P2P_DEVICE_NAME
description: WDI_TLV_P2P_DEVICE_NAME では、デバイス名を含む TLV です。
ms.assetid: 7FB04079-7F82-4D7B-95BA-45B5832B36C0
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_NAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ddf8dc3c5803ff805b49d3b36b8a656c25f4cce7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536733"
---
# <a name="wditlvp2pdevicename"></a>WDI\_TLV\_P2P\_デバイス\_名


WDI\_TLV\_P2P\_デバイス\_名がデバイス名を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x92

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                               |
|-----------|---------------------------------------------------------------------------|
| UINT8\[\] | デバイスのデバイス名を指定する UINT8 要素の配列。 |

 

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

 

 





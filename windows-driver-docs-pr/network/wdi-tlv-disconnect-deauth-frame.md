---
title: WDI_TLV_DISCONNECT_DEAUTH_FRAME
description: WDI_TLV_DISCONNECT_DEAUTH_FRAME では、受信した deauthentication フレームを含む TLV です。
ms.assetid: 394B83C7-D001-4816-BC38-42325469863C
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISCONNECT_DEAUTH_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: df28846ec9b8025079dfb1bde63eb7dfa2000f16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530467"
---
# <a name="wditlvdisconnectdeauthframe"></a>WDI\_TLV\_切断\_DEAUTH\_フレーム


WDI\_TLV\_切断\_DEAUTH\_フレームが受信した deauthentication フレームを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x37

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                                   |
|-----------|-------------------------------------------------------------------------------|
| UINT8\[\] | 受信した deauthentication フレームを含む UINT8 要素の配列。 |

 

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

 

 





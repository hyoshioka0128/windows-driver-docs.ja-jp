---
title: WDI_TLV_CHANNEL_WIDTH_LIST
description: WDI_TLV_CHANNEL_WIDTH_LIST では、チャネルの幅のリストを含む TLV です。
ms.assetid: 9869157D-2E71-4F08-92D0-A4FFA085ACE7
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHANNEL_WIDTH_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ce0aed396336af11a382a2673fbe7fb80d6389e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357659"
---
# <a name="wditlvchannelwidthlist"></a>WDI\_TLV\_チャネル\_幅\_一覧


WDI\_TLV\_チャネル\_幅\_リストは、チャネルの幅のリストを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xF5

## <a name="length"></a>長さ


Uint32 型の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型       | 説明                                 |
|------------|---------------------------------------------|
| UINT32\[\] | チャネル幅を (mhz) を指定の一覧。 |

 

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

 

 





---
title: WDI_TLV_PROBE_RESPONSE_FRAME
description: WDI_TLV_PROBE_RESPONSE_FRAME では、プローブ応答のフレームを含む TLV です。
ms.assetid: 600019AB-55D2-4EE1-9500-0AFCB07C3AB2
ms.date: 07/18/2017
keywords:
- WDI_TLV_PROBE_RESPONSE_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 236f92457eff0a98177101bd3812c7a8f231950a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342218"
---
# <a name="wditlvproberesponseframe"></a>WDI\_TLV\_プローブ\_応答\_フレーム


WDI\_TLV\_プローブ\_応答\_フレームは、プローブ応答フレームを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x9

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                         |
|-----------|---------------------------------------------------------------------|
| UINT8\[\] | プローブ応答フレームを指定する UINT8 要素の配列。 |

 

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

 

 





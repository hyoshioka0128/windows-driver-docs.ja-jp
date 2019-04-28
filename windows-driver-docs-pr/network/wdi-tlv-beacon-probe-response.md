---
title: WDI_TLV_BEACON_PROBE_RESPONSE
description: WDI_TLV_BEACON_PROBE_RESPONSE では、最新のビーコンまたは、ポートで受信したプローブ応答フレームを含む TLV です。
ms.assetid: D1148F9B-D25F-4AF0-8C55-43453441C667
ms.date: 07/18/2017
keywords:
- WDI_TLV_BEACON_PROBE_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6b1d741c6833a2f8453fac159bd6c952fcee80e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361986"
---
# <a name="wditlvbeaconproberesponse"></a>WDI\_TLV\_ビーコン\_プローブ\_応答


WDI\_TLV\_ビーコン\_プローブ\_応答が最新のビーコンまたは、ポートで受信したプローブ応答フレームを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x30

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 最新のビーコンまたは、ポートで受信したプローブ応答フレームを指定する UINT8 要素の配列。 これは、802.11 MAC ヘッダーには含まれません。 |

 

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

 

 





---
title: WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD
description: WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD では、到達不能検出のしきい値を含む TLV です。
ms.assetid: D2C41B26-90EF-4A62-A105-DBEF3822BA6E
ms.date: 07/18/2017
keywords:
- WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a557610cb4e19049936195e4dbe031b3e792d10b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573260"
---
# <a name="wditlvunreachabledetectionthreshold"></a>WDI\_TLV\_UNREACHABLE\_検出\_しきい値


WDI\_TLV\_UNREACHABLE\_検出\_しきい値が到達不能検出のしきい値を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xB1

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                                                                                                                                                                                               |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 到達不能検出のしきい値。 802.11 ステーションでは、ピア デバイスに接続が失われることを決定する前に、最大時間 (ミリ秒単位) で指定します。 ステーションはこの接続が失われるの決定を行うには欠落したビーコンを含める必要がありますが、し、必要なその他すべてのヒューリスティックを使用してもできます。 |

 

<a name="requirements"></a>必要条件
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

 

 





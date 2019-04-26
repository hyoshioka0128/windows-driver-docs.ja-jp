---
title: WDI_TLV_P2P_LISTEN_DURATION
description: WDI_TLV_P2P_LISTEN_DURATION は、Wi-Fi Direct を含む TLV は、実行時間情報をリッスンします。
ms.assetid: 6C14BB67-89E1-4795-9327-2B5B87BF2D7C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_LISTEN_DURATION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 105b45d743e363ad9e4eb043a6d39a2ab41efd85
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342596"
---
# <a name="wditlvp2plistenduration"></a>WDI\_TLV\_P2P\_リッスン\_期間


WDI\_TLV\_P2P\_リッスン\_期間は、Wi-Fi Direct リッスン期間情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xE9

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                                                    |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 時間 (ミリ秒) のリッスン サイクルです。 アダプターは、リッスン状態ではこの期間中にします。                                                           |
| UINT32 | 時間 (ミリ秒単位) をリッスン サイクル中にアクティブにリッスンするように、アダプターが必要です。 この期間は、リッスン サイクル時間未満である必要があります。 |

 

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

 

 





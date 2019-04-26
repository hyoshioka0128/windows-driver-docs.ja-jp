---
title: WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS では、Wi-Fi Direct 招待応答パラメーターを含む TLV です。
ms.assetid: A242F40C-D062-4A62-8F47-E42E74EAEFE8
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f49c1abdd25504eaedd2eee10dec81f3d19dfffc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347239"
---
# <a name="wditlvp2pinvitationresponseparameters"></a>WDI\_TLV\_P2P\_招待\_応答\_パラメーター


WDI\_TLV\_P2P\_招待\_応答\_パラメーターは、Wi-Fi Direct 招待応答パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x80

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                    |
|--------|--------------------------------------------------------------------------------|
| UINT8  | Wi-Fi Direct ステータス コード、Wi-Fi Direct の仕様で指定された. |
| UINT16 | 移動の構成のタイムアウト値 (ミリ秒)。                                 |
| UINT16 | クライアント構成のタイムアウト (ミリ秒)。                             |

 

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

 

 





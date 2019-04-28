---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT では、ピアに送信された操作フレームに関する情報を含む TLV です。
ms.assetid: DA469DF2-4C59-495C-A4B5-DC7B3B157566
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d73c9f22df88fee3ea81ac7d4c4b6abd0eaf68b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370946"
---
# <a name="wditlvp2psendactionframeresult"></a>WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果


WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_ピアに送信された操作フレームに関する情報を含む TLV になります。

## <a name="tlv-type"></a>TLV 型


0xAF

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                              | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                           |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果\_パラメーター**](wdi-tlv-p2p-send-action-frame-result-parameters.md) |                                |          | Wi-Fi Direct 操作フレーム結果パラメーターを送信します。 |
| [**WDI\_TLV\_P2P\_ACTION\_FRAME\_IES**](wdi-tlv-p2p-action-frame-ies.md)                                         |                                |          | I のセットは、リモート デバイスに送信されます。             |

 

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

 

 





---
title: WDI_TLV_P2P_LISTEN_CHANNEL
description: WDI_TLV_P2P_LISTEN_CHANNEL では、Wi-Fi Direct チャネル情報を含む TLV です。
ms.assetid: 45D1B507-C02B-432B-A552-78F2539ECE68
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_LISTEN_CHANNEL ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c341847563c60271e10069bc971dccf9039d1dde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552760"
---
# <a name="wditlvp2plistenchannel"></a>WDI\_TLV\_P2P\_リッスン\_チャネル


WDI\_TLV\_P2P\_リッスン\_チャネルは、Wi-Fi Direct チャネル情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x114

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                          | 説明                                                                        |
|-------------------------------|------------------------------------------------------------------------------------|
| UINT8\[3\]                    | クラスの動作とチャンネル番号が有効な国または地域コード。 |
| UINT8                         | チャンネル番号の動作のクラス/周波数帯。                         |
| WDI\_チャネル\_数 (UINT32) | Wi-Fi Direct デバイスまたはグループ チャンネル番号。                           |

 

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

 

 





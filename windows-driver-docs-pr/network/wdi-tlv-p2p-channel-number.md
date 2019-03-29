---
title: WDI_TLV_P2P_CHANNEL_NUMBER
description: WDI_TLV_P2P_CHANNEL_NUMBER では、Wi-Fi Direct チャネル番号情報を含む TLV です。
ms.assetid: CE17143E-5DA1-4F5B-A2E0-2BD480030129
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CHANNEL_NUMBER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d73f64587c46f1ecbeaf9f79c477d37f9ef84597
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572974"
---
# <a name="wditlvp2pchannelnumber"></a>WDI\_TLV\_P2P\_チャネル\_数


WDI\_TLV\_P2P\_チャネル\_番号は、Wi-Fi Direct チャネル番号情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x82

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                          | 説明                                                                        |
|-------------------------------|------------------------------------------------------------------------------------|
| UINT8\[3\]                    | クラスの動作とチャンネル番号が有効な国または地域コード。 |
| UINT8                         | チャンネル番号の動作のクラス/周波数帯。                         |
| WDI\_チャネル\_数 (UINT32) | Wi-Fi Direct デバイスまたはグループ チャンネル番号。                           |

 

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

 

 





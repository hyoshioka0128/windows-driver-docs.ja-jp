---
title: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS では、Wi-Fi Direct 操作フレーム応答パラメーターを含む TLV です。
ms.assetid: 2DFF00A6-FDE2-43EF-93C2-EEA3DBC00D52
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ff8624775cbd9e950a0967bbe68897dcdcad20f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539207"
---
# <a name="wditlvp2pactionframeresponseparameters"></a>WDI\_TLV\_P2P\_アクション\_フレーム\_応答\_パラメーター


WDI\_TLV\_P2P\_アクション\_フレーム\_応答\_パラメーターは、Wi-Fi Direct 操作フレーム応答パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xAD

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                                                    | 説明                                                                                                                          |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926086) | 送信する応答のフレームの型。                                                                                               |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)                       | ターゲットのピア Wi-Fi Direct デバイスのデバイスのアドレス。                                                                           |
| UINT8                                                                   | Wi-Fi Direct ダイアログ トークンこのトランザクションにします。                                                                                  |
| UINT32                                                                  | 送信タイムアウト。 この操作のフレームを送信するミリ秒単位で最大の時間を指定します。                                            |
| UINT32                                                                  | Post ACK 時間。 着信パケットの受信が確認した後をミリ秒単位でのリッスン チャネルで維持する時間を指定します。 |

 

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

 

 





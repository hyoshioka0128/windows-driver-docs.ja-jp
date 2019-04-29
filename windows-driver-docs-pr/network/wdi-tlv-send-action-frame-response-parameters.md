---
title: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS は、OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME のパラメーターを含む TLV です。
ms.assetid: F062F8A2-EEEF-4EFC-AEC8-F1D7AB13C899
ms.date: 07/18/2017
keywords:
- WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9a1855d75241425bdbd40ff113582b4bc986167a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330408"
---
# <a name="wditlvsendactionframeresponseparameters"></a>WDI\_TLV\_送信\_アクション\_フレーム\_応答\_パラメーター


WDI\_TLV\_送信\_アクション\_フレーム\_応答\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_送信\_応答\_アクション\_フレーム](https://msdn.microsoft.com/library/windows/hardware/dn925962)します。

## <a name="tlv-type"></a>TLV 型


0xE2

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                     |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WDI\_チャネル\_数 (UINT32)                     | 操作のフレームを送信し、として待機するチャネルは、post ACK 時間で指定します。                                    |
| WDI\_バンド\_ID (UINT32)                            | 操作のフレームを送信するためのバンドの ID。                                                                                           |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | ターゲットへのアクセスの MAC アドレスは、ポイントまたはアダプターをピアリングします。                                                                                     |
| UINT32                                            | 送信タイムアウト。 この操作のフレームを送信する最大時間 (ミリ秒単位) を指定します。                                                       |
| UINT32                                            | 後の受信確認応答時間。 着信パケットの受信が確認された後に、チャネルのリッスンに保たれます (ミリ秒) を指定します。 |

 

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

 

 





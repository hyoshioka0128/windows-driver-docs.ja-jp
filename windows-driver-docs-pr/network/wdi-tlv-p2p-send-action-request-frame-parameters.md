---
title: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS は、OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME を使用して Wi-fi ダイレクトアクション要求フレームを送信するためのパラメーターを含む TLV です。
ms.assetid: 802654D0-CC8E-4808-8C1B-BAAF4C6E53F1
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 394e7f138bfa37e1bb86fad26b8b66e81308088d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845125"
---
# <a name="wdi_tlv_p2p_send_action_request_frame_parameters"></a>WDI\_TLV\_P2P\_\_アクション\_要求\_フレーム\_パラメーターを送信します


WDI\_TLV\_P2P\_SEND\_ACTION\_要求\_フレーム\_パラメーターは、 [OID\_WDI\_タスクを使用して Wi-fi ダイレクトアクション要求フレームを送信するためのパラメーターを含む TLV\_P2P\_\_要求\_アクション\_フレームに送信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame)します。

## <a name="tlv-type"></a>TLV 型


0x8B

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                    | 説明                                                                                                                    |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 送信する要求の種類。                                                                                                   |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | ターゲットピアデバイスの MAC アドレス。                                                                                     |
| UINT8                                                                   | トランザクションの直接ダイアログトークン。                                                                                   |
| UINT32                                                                  | 送信タイムアウト。 アクションフレームを送信する最大時間 (ミリ秒単位)。                                                 |
| UINT32                                                                  | ACK 後の熟考時間。 受信パケットが受信確認された後にリッスンチャネルに保持する時間 (ミリ秒単位)。 |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 





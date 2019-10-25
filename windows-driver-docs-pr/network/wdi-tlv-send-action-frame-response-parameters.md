---
title: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS は、OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME のパラメーターを含む TLV です。
ms.assetid: F062F8A2-EEEF-4EFC-AEC8-F1D7AB13C899
ms.date: 07/18/2017
keywords:
- WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 2319c333a501dc34ef8678d942470a3bd38c6a4f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841732"
---
# <a name="wdi_tlv_send_action_frame_response_parameters"></a>WDI\_TLV\_送信\_アクション\_フレーム\_応答\_パラメーター


WDI\_TLV\_SEND\_ACTION\_FRAME\_RESPONSE\_PARAMETERS は、 [OID\_WDI\_TASK\_send\_response\_ACTION のパラメーターを含む TLV です\_フレーム](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-send-response-action-frame)。

## <a name="tlv-type"></a>TLV 型


0xE2

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                     |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WDI\_CHANNEL\_NUMBER (UINT32)                     | アクションフレームを送信するチャネル、および確認後の熟考時間で指定されたとおりに待機するチャネル。                                    |
| WDI\_バンド\_ID (UINT32)                            | アクションフレームを送信するバンドの ID。                                                                                           |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ターゲットアクセスポイントまたはピアアダプターの MAC アドレス。                                                                                     |
| UINT32                                            | 送信タイムアウト。 このアクションフレームを送信する最大時間 (ミリ秒) を指定します。                                                       |
| UINT32                                            | 受信確認後の熟考時間。 受信パケットが受信確認された後にリッスンチャネルに保持する時間 (ミリ秒単位) を指定します。 |

 

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

 

 





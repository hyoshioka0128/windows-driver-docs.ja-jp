---
title: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS は、OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME のパラメーターを含む TLV です。
ms.assetid: 92629752-A94B-442A-97E9-D8E1C7924855
ms.date: 07/18/2017
keywords:
- WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: fb474ec370af02e8d51873b0aed4fccf55bc098f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841735"
---
# <a name="wdi_tlv_send_action_frame_request_parameters"></a>WDI\_TLV\_送信\_アクション\_フレーム\_要求\_パラメーター


WDI\_TLV\_SEND\_ACTION\_FRAME\_REQUEST\_PARAMETERS は、 [OID\_WDI\_TASK\_send\_request\_ACTION のパラメーターを含む TLV です\_フレーム](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-send-request-action-frame)。

## <a name="tlv-type"></a>TLV 型


0xBF

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

 

 





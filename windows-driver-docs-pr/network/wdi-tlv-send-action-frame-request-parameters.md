---
title: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS は、OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME のパラメーターを含む TLV です。
ms.assetid: 92629752-A94B-442A-97E9-D8E1C7924855
ms.date: 07/18/2017
keywords:
- WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d61fea96329da1bc96abdc495994a6a960b54e3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362833"
---
# <a name="wditlvsendactionframerequestparameters"></a>WDI\_TLV\_送信\_アクション\_フレーム\_要求\_パラメーター


WDI\_TLV\_送信\_アクション\_フレーム\_要求\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_送信\_要求\_アクション\_フレーム](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-send-request-action-frame)します。

## <a name="tlv-type"></a>TLV 型


0xBF

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                     |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WDI\_チャネル\_数 (UINT32)                     | 操作のフレームを送信し、として待機するチャネルは、post ACK 時間で指定します。                                    |
| WDI\_バンド\_ID (UINT32)                            | 操作のフレームを送信するためのバンドの ID。                                                                                           |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | ターゲットへのアクセスの MAC アドレスは、ポイントまたはアダプターをピアリングします。                                                                                     |
| UINT32                                            | 送信タイムアウト。 この操作のフレームを送信する最大時間 (ミリ秒単位) を指定します。                                                       |
| UINT32                                            | 後の受信確認応答時間。 着信パケットの受信が確認された後に、チャネルのリッスンに保たれます (ミリ秒) を指定します。 |

 

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

 

 





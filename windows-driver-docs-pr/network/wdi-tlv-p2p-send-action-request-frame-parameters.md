---
title: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS は、OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME で Wi-Fi Direct アクション要求フレームを送信するためのパラメーターを含む TLV です。
ms.assetid: 802654D0-CC8E-4808-8C1B-BAAF4C6E53F1
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 32fdbe11f8d4b10d0b6ebeac4d59018fd5044150
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355431"
---
# <a name="wditlvp2psendactionrequestframeparameters"></a>WDI\_TLV\_P2P\_送信\_アクション\_要求\_フレーム\_パラメーター


WDI\_TLV\_P2P\_送信\_アクション\_要求\_フレーム\_パラメーターでWi-FiDirectアクション要求フレームを送信するためのパラメーターを含むTLVは、[OID\_WDI\_タスク\_P2P\_送信\_要求\_アクション\_フレーム](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame)します。

## <a name="tlv-type"></a>TLV 型


0x8B

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                    | 説明                                                                                                                    |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 送信する要求の種類。                                                                                                   |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | ターゲットのピア デバイスの MAC アドレス。                                                                                     |
| UINT8                                                                   | 直接ダイアログ トークン トランザクション。                                                                                   |
| UINT32                                                                  | 送信タイムアウト。 最大時間 (ミリ秒)、アクションのフレームを送信します。                                                 |
| UINT32                                                                  | Post ACK 時間。 時間 (ミリ秒) で、着信パケットの受信が確認された後に、listen チャネルに保たれます。 |

 

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

 

 





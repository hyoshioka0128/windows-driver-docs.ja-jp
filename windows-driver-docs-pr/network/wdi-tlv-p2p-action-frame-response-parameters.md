---
title: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS は、Wi-fi ダイレクトアクションフレームの応答パラメーターを含む TLV です。
ms.assetid: 2DFF00A6-FDE2-43EF-93C2-EEA3DBC00D52
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 90d026eac9fa442263baff118ff42537f7247f30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824352"
---
# <a name="wdi_tlv_p2p_action_frame_response_parameters"></a>WDI\_TLV\_P2P\_ACTION\_FRAME\_RESPONSE\_PARAMETERS


WDI\_TLV\_P2P\_ACTION\_FRAME\_RESPONSE\_PARAMETERS は Wi-fi Direct Action Frame response parameters を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xAD

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                    | 説明                                                                                                                          |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 送信される応答フレームの種類。                                                                                               |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | ターゲットピア Wi-fi ダイレクトデバイスのデバイスアドレス。                                                                           |
| UINT8                                                                   | このトランザクションの Wi-fi ダイレクトダイアログトークン。                                                                                  |
| UINT32                                                                  | 送信タイムアウト。 このアクションフレームを送信する最大時間をミリ秒単位で指定します。                                            |
| UINT32                                                                  | ACK 後の熟考時間。 受信パケットが受信確認された後にリッスンチャネルに保持する時間をミリ秒単位で指定します。 |

 

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

 

 





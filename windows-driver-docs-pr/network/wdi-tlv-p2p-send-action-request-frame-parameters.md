---
title: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS は、OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME で Wi-Fi Direct アクション要求フレームを送信するためのパラメーターを含む TLV です。
ms.assetid: 802654D0-CC8E-4808-8C1B-BAAF4C6E53F1
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 77a4163e1ecd2c9bf08ae72a378bfa4badf4cd1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384507"
---
# <a name="wditlvp2psendactionrequestframeparameters"></a>WDI\_TLV\_P2P\_送信\_アクション\_要求\_フレーム\_パラメーター


WDI\_TLV\_P2P\_送信\_アクション\_要求\_フレーム\_パラメーターでWi-FiDirectアクション要求フレームを送信するためのパラメーターを含むTLVは、[OID\_WDI\_タスク\_P2P\_送信\_要求\_アクション\_フレーム](https://msdn.microsoft.com/library/windows/hardware/dn925956)します。

## <a name="tlv-type"></a>TLV 型


0x8B

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                    | 説明                                                                                                                    |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_アクション\_フレーム\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926086) | 送信する要求の種類。                                                                                                   |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)                       | ターゲットのピア デバイスの MAC アドレス。                                                                                     |
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

 

 





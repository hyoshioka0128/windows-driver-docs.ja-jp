---
title: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS は、OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME のパラメーターを含む TLV です。
ms.assetid: 92629752-A94B-442A-97E9-D8E1C7924855
ms.date: 07/18/2017
keywords:
- WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a738c99384c123d429986f2cb0f5e58f654c5516
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553270"
---
# <a name="wditlvsendactionframerequestparameters"></a>WDI\_TLV\_送信\_アクション\_フレーム\_要求\_パラメーター


WDI\_TLV\_送信\_アクション\_フレーム\_要求\_パラメーターはパラメーターを含む TLV [OID\_WDI\_タスク\_送信\_要求\_アクション\_フレーム](https://msdn.microsoft.com/library/windows/hardware/dn925961)します。

## <a name="tlv-type"></a>TLV 型


0xBF

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                              | 説明                                                                                                                                     |
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

 

 





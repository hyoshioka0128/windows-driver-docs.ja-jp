---
title: NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED を使用して、Wi-Fi Direct アクションのフレームが受信されたことを示します。
ms.assetid: 16e8f61d-373b-49fb-a0c5-4505fa7e653d
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_P2P_ACTION_FRAME_RECEIVED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 042bf4c394103a7b89c65ec3b3940bd06f348ed4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390673"
---
# <a name="ndisstatuswdiindicationp2pactionframereceived"></a>NDIS\_状態\_WDI\_INDICATION\_P2P\_アクション\_フレーム\_受信日時


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_P2P\_アクション\_フレーム\_を Wi-Fi Direct アクションのフレームが受信されたことを示すために受信します。

| オブジェクト |
|--------|
| ポート   |

 

ホストが発行することがあります、 [OID\_WDI\_タスク\_P2P\_送信\_応答\_アクション\_フレーム](oid-wdi-task-p2p-send-response-action-frame.md)この要求。

ポートは、これらのパケットで、次の状況のいずれかを示す必要があります。

-   ポートがリッスン状態です。
-   ポートは、GO を動作状態には。
-   リモートのリッスン ポートがもたらすチャネルの場合に、 [OID\_WDI\_タスク\_P2P\_送信\_要求\_アクション\_フレーム](oid-wdi-task-p2p-send-request-action-frame.md)または[OID\_WDI\_タスク\_P2P\_送信\_応答\_アクション\_フレーム](oid-wdi-task-p2p-send-response-action-frame.md)最近発行されました。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_受信\_フレーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn897957) |                                |          | 受信アクションのフレームを Wi-Fi Direct 情報。 この情報は、ホストを発行すると、ポートに転送されます[OID\_WDI\_タスク\_P2P\_送信\_応答\_アクション\_フレーム](oid-wdi-task-p2p-send-response-action-frame.md). |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_タスク\_P2P\_送信\_要求\_アクション\_フレーム](oid-wdi-task-p2p-send-request-action-frame.md)

[OID\_WDI\_TASK\_P2P\_SEND\_RESPONSE\_ACTION\_FRAME](oid-wdi-task-p2p-send-response-action-frame.md)

 

 





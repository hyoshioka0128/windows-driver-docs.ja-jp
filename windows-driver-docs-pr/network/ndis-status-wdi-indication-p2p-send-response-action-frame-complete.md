---
title: NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE を使用して、OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME によって送信された応答アクション フレームに関する情報を示します。
ms.assetid: 0b330ad6-4a55-4a3e-951f-0e5a951a8cf1
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_P2P_SEND_RESPONSE_ACTION_FRAME_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2780d122bb0ebb6ade3baaa7a0800b0a02d3b6d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360199"
---
# <a name="ndisstatuswdiindicationp2psendresponseactionframecomplete"></a>NDIS\_状態\_WDI\_INDICATION\_P2P\_送信\_応答\_アクション\_フレーム\_完了


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_P2P\_送信\_応答\_アクション\_フレーム\_を示すために完了によって送信された応答アクション フレームに関する情報[OID\_WDI\_タスク\_P2P\_送信\_応答\_アクション\_フレーム](oid-wdi-task-p2p-send-response-action-frame.md).

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                                       | 許可されている複数の TLV インスタンス | 省略可能                                            | 説明                                                            |
|------------------------------------------------------------------------------------------------------------|--------------------------------|-----------------------------------------------------|------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果**](https://msdn.microsoft.com/library/windows/hardware/dn897993) |                                | この TLV は、のみ成功したかどうか、状態には必要です。 | ピアに送信された応答アクション フレームに関する情報。 |

 

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

 

 





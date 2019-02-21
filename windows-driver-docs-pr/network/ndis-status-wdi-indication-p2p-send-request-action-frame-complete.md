---
title: NDIS_STATUS_WDI_INDICATION_P2P_SEND_REQUEST_ACTION_FRAME_COMPLETE
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_P2P_SEND_REQUEST_ACTION_FRAME_COMPLETE を使用して、OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME によって送信された要求のアクション フレームに関する情報を示します。
ms.assetid: 4c67b512-456f-48ed-bd1c-71a32bcf85f0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_P2P_SEND_REQUEST_ACTION_FRAME_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d4a8610da1562236a1a2c3a648b56b31c9da903e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537938"
---
# <a name="ndisstatuswdiindicationp2psendrequestactionframecomplete"></a>NDIS\_状態\_WDI\_INDICATION\_P2P\_送信\_要求\_アクション\_フレーム\_完了


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_P2P\_送信\_要求\_アクション\_フレーム\_を示すために完了によって送信された要求のアクション フレームに関する情報[OID\_WDI\_タスク\_P2P\_送信\_要求\_アクション\_フレーム](oid-wdi-task-p2p-send-request-action-frame.md).

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                                       | 許可されている複数の TLV インスタンス | 省略可能                                            | 説明                                                           |
|------------------------------------------------------------------------------------------------------------|--------------------------------|-----------------------------------------------------|-----------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_送信\_アクション\_フレーム\_結果**](https://msdn.microsoft.com/library/windows/hardware/dn897993) |                                | この TLV は、のみ成功したかどうか、状態には必要です。 | ピアに送信された要求のアクション フレームに関する情報。 |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 





---
title: OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME
description: OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME は、デバイス アクションのフレーム要求に送信する別のデバイスを要求します。
ms.assetid: CAC86B50-BE85-4650-B6D3-738B4E960587
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 30d19184ac34a7410df06a082b676f39ec47fd0e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548750"
---
# <a name="oidwditasksendrequestactionframe"></a>OID\_WDI\_タスク\_送信\_要求\_アクション\_フレーム


OID\_WDI\_タスク\_送信\_要求\_アクション\_フレームは、デバイス アクションのフレーム要求に送信する別のデバイスを要求します。

| オブジェクト | 中止できます。                                           | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 ポートは、中止した後、クリーンな状態でなければなりません。 | 3                                     | 5                               |

 

このコマンドは、異なる[OID\_WDI\_タスク\_送信\_応答\_アクション\_フレーム](oid-wdi-task-send-response-action-frame.md)、これは非常に多く時間を区別します。操作です。

デバイスは、要求フレームの受信確認を受信するとタスクのパラメーターで指定されている投稿確認について詳しく説明に、同じチャネルについて熟考ものとし、受信し、それ自体を処理しないすべてアクション フレームをホストに示すものとします。

最大のタイムアウトの期限が切れていない限り、デバイスはパブリック アクション フレームを送信するリモート デバイスのリッスン チャネル上のリモート デバイスを再試行してください。

タスクが完了するかローカル デバイス送信された操作フレーム用のリモート デバイスからの受信確認を受信すると、タイムアウトになると、またはホストは、操作を中止します。 デバイスは、同じチャネル時間の有効期限が切れた後、タスクの完了にすることがあります。

ホストは、この操作を中止し、続行/再試行、パブリック アクション フレーム交換できるようになりますが、デバイスがすぐにこの操作を中止することがある重要なことがあります。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                     |
|-----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_送信\_アクション\_フレーム\_要求\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/dn898053) |                                |          | アクションのフレーム要求を送信するためのパラメーターです。 |
| [**WDI\_TLV\_アクション\_フレーム\_本文**](https://msdn.microsoft.com/library/windows/hardware/dn926118)                                         |                                |          | アクションのフレームの本文。                          |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_送信\_要求\_アクション\_フレーム\_完了](ndis-status-wdi-indication-send-request-action-frame-complete.md)要件
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

 

 





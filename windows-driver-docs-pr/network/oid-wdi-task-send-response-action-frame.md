---
title: OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME
description: OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME は、IHV コンポーネントからの応答アクションのフレームを送信することを要求します。
ms.assetid: DA2FF006-BA81-48B9-8AAD-694818E78AEF
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f05257da5bda2ea345898376b93c4f97d37fb275
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387224"
---
# <a name="oidwditasksendresponseactionframe"></a>OID\_WDI\_タスク\_送信\_応答\_アクション\_フレーム


OID\_WDI\_タスク\_送信\_応答\_アクション\_フレームは IHV コンポーネントからの応答アクションのフレームを送信することを要求します。

| オブジェクト | 中止できます。                                           | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 ポートは、中止した後、クリーンな状態でなければなりません。 | 3                                     | 5                               |

 

このタスクは、時間的制約が、このパケットの受信の 100 ミリ秒以内に処理する必要があります。

最大のタイムアウトの期限が切れていないときに、ポートは、フレームを指定したチャネル上のリモート デバイスに送信をやり直してください。

タスクが完了するかローカル デバイス送信された操作フレーム用のリモート デバイスからの受信確認を受信すると、タイムアウトになると、またはホストは、操作を中止します。 デバイスは、同じチャネル時間の有効期限が切れた後、タスクの完了にすることがあります。

ホストは、この操作を中止し、続行/再試行アクション フレーム、交換できるようになりますが、デバイスがすぐにこの操作を中止することがある重要なことがあります。

## <a name="task-parameters"></a>タスク パラメーター


| TLV                                                                                                               | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                      |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------|
| [**WDI\_TLV\_送信\_アクション\_フレーム\_応答\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-send-action-frame-response-parameters) |                                |          | アクションのフレームの応答を送信するためのパラメーターです。 |
| [**WDI\_TLV\_アクション\_フレーム\_本文**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-action-frame-body)                                           |                                |          | アクションのフレームの本文。                           |

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_送信\_応答\_アクション\_フレーム\_完了](ndis-status-wdi-indication-send-response-action-frame-complete.md)

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

 

 





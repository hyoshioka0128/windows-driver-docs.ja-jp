---
title: 通知エラー
description: 通知エラー
ms.assetid: ffead40c-5c1c-45f6-83d2-48e4af357255
keywords:
- スプーラ通知 WDK の印刷、エラー
- 印刷スプーラ通知 WDK、エラー
- 通知エラー WDK 印刷スプーラー
- エラー WDK スプーラー通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e19431dbecdea7e366840bbaa8e7951b19c487
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339891"
---
# <a name="notification-errors"></a>通知エラー





メンバー、 **PrintAsyncNotifyError**列挙型が発生したエラーの種類を示すために使用されます。 次の表では、想定されるエラー コードについて説明します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>エラー コード</th>
<th>値</th>
<th>通信の種類</th>
<th>対象</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CHANNEL_CLOSED_BY_SERVER</p></td>
<td><p>0x01</p></td>
<td></td>
<td></td>
<td><p><strong>SendNotification</strong>と<strong>CloseChannel</strong>印刷スプーラーには、呼び出しの前に、チャネルが閉じられたときに、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_CLOSED_BY_ANOTHER_LISTENER</p></td>
<td><p>0x02</p></td>
<td><p>双方向</p></td>
<td><p>Listener</p></td>
<td><p>SendNotification と<strong>CloseChannel</strong>別のリスナーには、呼び出しの前に、チャネルが閉じられたときに、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_CLOSED_BY_SAME_LISTENER</p></td>
<td><p>0x03</p></td>
<td><p>双方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>CloseChannel</strong>同一のリスナーには、呼び出しの前に、チャネルが閉じられたときに、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_RELEASED_BY_LISTENER</p></td>
<td><p>0x04</p></td>
<td></td>
<td></td>
<td><p><strong>SendNotification</strong>と<strong>CloseChannel</strong>別のリスナーには、呼び出しの前に、チャネルがリリースされたときに、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>UNIRECTIONAL_NOTIFICATION_LOST</p></td>
<td><p>0x05</p></td>
<td><p>一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong> 1 つ以上存在するリスナーの通知を受信しなかったため、送信者にこの値を返します。 これは、送信者が、リスナーが処理できるよりも速く通知を送信するときに発生します。</p></td>
</tr>
<tr class="even">
<td><p>ASYNC_NOTIFICATION_FAILURE</p></td>
<td><p>0x06</p></td>
<td><p>一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong>存在するリスナーのいずれも通知を受け取るときに、送信者にこの値を返します。 この状況は、いくつかの制限付きのシステム リソースの状態で発生することができます.</p></td>
</tr>
<tr class="odd">
<td><p>NO_LISTENERS</p></td>
<td><p>0x07</p></td>
<td><p>一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong>リスナーが登録されていないことを示す非エラーとしての送信者にこの値を返します。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_ALREADY_CLOSED</p></td>
<td><p>0x08</p></td>
<td><p>双方向</p></td>
<td><p>送信者とリスナー</p></td>
<td><p><strong>SendNotification</strong>チャネルが既にに閉じられたときに、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_ALREADY_OPENED</p></td>
<td><p>0x09</p></td>
<td><p>双方向と一方向</p></td>
<td><p>送信者とリスナー</p></td>
<td><p><strong>CreateNotificationChannel</strong>チャネルが既に開いているときに、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_WAITING_FOR_CLIENT_NOTIFICATION</p></td>
<td><p>0x0a</p></td>
<td><p>双方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong>チャネルがクライアント通知を待機しているときに、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_NOT_OPENED</p></td>
<td><p>0x0b</p></td>
<td><p>双方向と一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>CreateNotificationChannel</strong>チャネルが開かれていない場合は、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>ASYNC_CALL_ALREADY_PARKED</p></td>
<td><p>0x0c</p></td>
<td><p>双方向と一方向</p></td>
<td><p></p>
送信者 (内部)</td>
<td><p>呼び出しがこのチャネルで既にされています。 一度にチャネルあたり 1 つ以上の呼び出しが許可されていません。</p></td>
</tr>
<tr class="odd">
<td><p>NOT_REGISTERED</p></td>
<td><p>0x0d</p></td>
<td></td>
<td></td>
<td><p><strong>UnregisterForNotifications</strong>登録オブジェクトが登録されていない場合は、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>ALREADY_UNREGISTERED</p></td>
<td><p>0x0e</p></td>
<td><p>双方向と一方向</p></td>
<td><p>Listener</p></td>
<td><p><strong>UnregisterForNotifications</strong>登録オブジェクトが既に登録されている場合は、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>ALREADY_REGISTERED</p></td>
<td><p>0x0f</p></td>
<td><p>双方向と一方向</p></td>
<td><p>Listener</p></td>
<td><p><strong>RegisterForNotifications</strong>登録オブジェクトは既に登録されているときに、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_ACQUIRED</p></td>
<td><p>0x10</p></td>
<td><p>双方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong>と<strong>CloseChannel</strong>別のリスナー チャネルを取得するときに、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>ASYNC_CALL_IN_PROGRESS</p></td>
<td><p>0x11</p></td>
<td><p>双方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong>呼び出しが既に進行中の場合、この値を返します。 チャネルあたり 1 つだけの呼び出しは一度に実行できます。</p></td>
</tr>
<tr class="even">
<td><p>MAX_NOTIFICATION_SIZE_EXCEEDED</p></td>
<td><p>0x12</p></td>
<td><p>双方向と一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong>通知データのサイズが許容される最大を超えた場合に、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>INTERNAL_NOTIFICATION_QUEUE_IS_FULL</p></td>
<td><p>0x13</p></td>
<td><p>双方向と一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>OnEventNotify</strong>通知キューがいっぱいになったときに、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>INVALID_NOTIFICATION_TYPE</p></td>
<td><p>0x14</p></td>
<td><p>双方向と一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>SendNotification</strong>通知の種類が、チャネルの種類とは異なる場合は、この値を返します。</p></td>
</tr>
<tr class="odd">
<td><p>MAX_REGISTRATION_COUNT_EXCEEDED</p></td>
<td><p>0x15</p></td>
<td><p>双方向と一方向</p></td>
<td><p>Listener</p></td>
<td><p><strong>RegisterForNotifications</strong>登録の数が許可されている最大数を超えると、この値を返します。</p></td>
</tr>
<tr class="even">
<td><p>MAX_CHANNEL_COUNT_EXCEEDED</p></td>
<td><p>0x16</p></td>
<td><p>双方向と一方向</p></td>
<td><p>送信者</p></td>
<td><p><strong>CreatePrintNotificationChannel</strong>チャネルの数が許可されている最大数を超えると、この値を返します。</p></td>
</tr>
</tbody>
</table>

 

 

 





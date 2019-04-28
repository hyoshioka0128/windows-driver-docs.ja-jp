---
title: ストリーム要求ブロックの処理
description: ストリーム要求ブロックの処理
ms.assetid: fb4fda0d-54e9-4f1b-a78c-276e770189d5
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルされる Srb
- ミニドライバー WDK Windows 2000 のカーネルされる Srb のストリーミング
- WDK Windows 2000 カーネル ストリーミング、ミニドライバーされる Srb
- される Srb WDK ストリーミング ミニドライバー
- ストリーム要求のブロックを参照してください SRB またはされる Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bc06328637c53119e378c9a8ef9b381d2a267c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363604"
---
# <a name="handling-stream-request-blocks"></a>ストリーム要求ブロックの処理





オペレーティング システムでは、クラス ドライバーのデバイス上のすべての I/O 要求をディスパッチします。 クラス ドライバーは、ハードウェアに固有の情報をミニドライバーから、ミニドライバーにされる Srb を渡すことによってさらに要求します。 クラスのドライバーが要求の操作を指定します、**コマンド**ストリーム要求のブロックのメンバー。

全体としてミニドライバーと、ミニドライバー内の各ストリームの両方には、I/O 要求がある場合があります。 ようにミニドライバーに提供する必要があります、 [ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)デバイス全体にわたる要求を処理するルーチン。 各ストリームは、I/O 要求を処理するために 2 つのルーチンをサポートする必要があります。 1 つのデータ要求、およびに対する制御要求の 1 つ。 クラス ドライバーはデータ要求のコールバックを呼び出す[ *StrMiniReceiveStreamDataPacket*](https://msdn.microsoft.com/library/windows/hardware/ff568470)を処理するには、すべて読み取りし、書き込みストリームを要求します。 ストリームの他のすべての要求に渡される[ **StrMiniReceiveStreamControlPacket**](https://msdn.microsoft.com/library/windows/hardware/ff568467)します。

クラス ドライバーは、ミニドライバーの同期を処理する場合、ストリームの要求をキューし、一度に 1 つミニドライバーにディスパッチします。 クラス ドライバーが 3 つの独立したキュー - デバイスの要求の 1 つを保持し、ストリーム データとコントロールの 1 つずつを要求します。 ミニドライバーは、準備ができているからこれらのキューの 1 つの新しい要求を次のように信号可能性があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>要求の種類</th>
<th>ルーチン</th>
<th>ルーチンの NotificationType パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>デバイスの要求</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568239" data-raw-source="[&lt;strong&gt;StreamClassDeviceNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568239)"><strong>StreamClassDeviceNotification</strong></a></p></td>
<td><p>ReadyForNextDeviceRequest</p></td>
</tr>
<tr class="even">
<td><p>ストリームの制御の要求</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568266" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568266)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamControlRequest</p></td>
</tr>
<tr class="odd">
<td><p>ストリームのデータ要求</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568266" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568266)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamDataRequest</p></td>
</tr>
</tbody>
</table>

 

クラスのドライバーを呼び出すと**StrMiniReceive*XXX*パケット**ミニドライバーにストリーム要求のブロックを渡します。 ミニドライバーのルーチンは、要求が完了しなかったクラス ドライバーに通知するまでに、ストリーム要求のブロックを唯一のアクセス権を持ちます。

ミニドライバーは、要求の処理が完了したら、必要がありますシグナル クラス ドライバー次のように、要求が完了します。

1.  ミニドライバーは、要求の状態を設定する必要があります、**状態**ストリーム要求のブロックのフィールド。

2.  ミニドライバーは呼び出すことによって、要求が完了したことを通知する必要があります[ **StreamClassDeviceNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff568239)または[ **StreamClassStreamNotification**](https://msdn.microsoft.com/library/windows/hardware/ff568266). デバイスの要求をミニドライバーの呼び出しを完了する**StreamClassDeviceNotification**で、 *NotificationType* DeviceRequestComplete のパラメーター。 ストリーム要求をミニドライバーの呼び出しを完了する**StreamClassStreamNotification**で、 *NotificationType* StreamRequestComplete のパラメーター。

3.  クラスのドライバーが、同期を処理し、ミニドライバーがまだシグナル状態にならないクラス ドライバーがこのキューで別の要求を可能である場合は、その必要がありますようになりました。

ミニドライバーは呼び出すことによって 2 および 3 を組み合わせることができます[ **StreamClassCompleteRequestAndMarkQueueReady**](https://msdn.microsoft.com/library/windows/hardware/ff568232)します。

ミニドライバーは、クラス ドライバーは、タイムアウト要求をキャンセルする必要がありますので、非同期的に要求を処理します。 これらの目的で、ミニドライバーを提供する必要があります、 [ *StrMiniCancelPacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568448)と[ *StrMiniRequestTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff568473)ルーチン。 クラス ドライバーは、キャンセルまたは要求がタイムアウトするときにそれぞれミニドライバー ルーチンを呼び出します。

オペレーティング システムによって基になる I/O 要求が取り消されたときに、クラス ドライバーは、要求をキャンセルします。 クラスのドライバーがタイムアウトになる時間がかかりすぎる--を処理する要求がで要求をタイムアウトするまでの秒数のカウンターをデクリメント、 **TimeoutCounter**ストリーム要求のブロックのメンバー。 設定する必要がありますが、ミニドライバーは、長期間の要求の処理を延期する必要がある場合、 **TimeoutCounter** 0--メンバー クラス ドライバーしはタイムアウトしません要求。 それをリセットする必要があります、ミニドライバーに要求の処理が再開される**TimeoutCounter**に等しい、 **TimeoutOriginal**ストリーム要求のブロックのメンバー。 ミニドライバーをリセットできます**TimeoutOriginal**要求がタイムアウトするまでの時間の長さを変更します。参照してください[ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)詳細についてはします。

 

 





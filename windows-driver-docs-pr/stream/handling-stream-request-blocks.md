---
title: ストリーム要求ブロックの処理
description: ストリーム要求ブロックの処理
ms.assetid: fb4fda0d-54e9-4f1b-a78c-276e770189d5
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、SRBs
- streaming ミニドライバー WDK Windows 2000 カーネル、SRBs
- ミニドライバー WDK Windows 2000 カーネルストリーミング、SRBs
- SRBs WDK streaming ミニドライバー
- ストリーム要求ブロック SRB または SRBs を参照してください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8c9124139fc78e12a312221c99148b4fdf0c23a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837958"
---
# <a name="handling-stream-request-blocks"></a>ストリーム要求ブロックの処理





オペレーティングシステムは、デバイス上のすべての i/o 要求をクラスドライバーにディスパッチします。 クラスドライバーは、SRBs をミニドライバーに渡すことによって、ミニドライバーからハードウェア固有の情報を要求します。 クラスドライバーは、ストリーム要求ブロックの**コマンド**メンバーで要求する操作を指定します。

ミニドライバーの全体と、ミニドライバー内の各ストリームは、i/o 要求を受け取ることができます。 ミニドライバーは、デバイス全体の要求を処理するために、 [*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)ルーチンを提供する必要があります。 各ストリームは、i/o 要求を処理する2つのルーチンをサポートする必要があります。1つはデータ要求用で、もう1つは制御要求用です。 クラスドライバーは、データ要求のコールバック[*StrMiniReceiveStreamDataPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)を呼び出して、ストリームのすべての読み取り要求と書き込み要求を処理します。 ストリームに対する他のすべての要求は、 [**StrMiniReceiveStreamControlPacket**](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85))に渡されます。

クラスドライバーがミニドライバーの同期を処理している場合は、ストリーム要求をキューに置いて、一度に1つずつミニドライバーにディスパッチします。 クラスドライバーは、デバイス要求用に1つ、ストリームデータと制御要求用にそれぞれ1つずつ、3つの個別のキューを保持します。 ミニドライバーは、次のように、キューのいずれかからの新しい要求の準備ができたことを通知する場合があります。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdevicenotification" data-raw-source="[&lt;strong&gt;StreamClassDeviceNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdevicenotification)"><strong>StreamClassDeviceNotification</strong></a></p></td>
<td><p>ReadyForNextDeviceRequest</p></td>
</tr>
<tr class="even">
<td><p>ストリームコントロール要求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamControlRequest</p></td>
</tr>
<tr class="odd">
<td><p>ストリームデータ要求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamDataRequest</p></td>
</tr>
</tbody>
</table>

 

クラスドライバーは、 **Strminireceive*XXX*パケット**を呼び出すと、ストリーム要求ブロックをミニドライバーに渡します。 ミニドライバーのルーチンは、要求を完了したことをクラスドライバーに通知するまで、ストリーム要求ブロックにのみアクセスできます。

ミニドライバーが要求の処理を完了すると、次のように要求を完了したことをクラスドライバーに通知する必要があります。

1.  ミニドライバーは、要求の状態をストリーム要求ブロックの**status**フィールドに設定する必要があります。

2.  ミニドライバーは、 [**StreamClassDeviceNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdevicenotification)または[**Streamclassstreamnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)を呼び出して、要求を完了したことを通知する必要があります。 デバイス要求を完了するために、ミニドライバーは DeviceRequestComplete の*NotificationType*パラメーターを使用して**StreamClassDeviceNotification**を呼び出します。 ストリーム要求を完了するために、ミニドライバーは**Streamclassstreamnotification**を呼び出します。 StreamRequestComplete の*NotificationType*パラメーターを指定します。

3.  クラスドライバーが同期を処理していて、ミニドライバーが、このキューで別の要求の準備ができていることをクラスドライバーに通知していない場合は、ここで実行する必要があります。

ミニドライバーでは、 [**StreamClassCompleteRequestAndMarkQueueReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscompleterequestandmarkqueueready)を呼び出すことによって2と3を組み合わせることができます。

ミニドライバーは要求を非同期的に処理するため、クラスドライバーは要求をキャンセルまたはタイムアウトする必要がある場合があります。 このため、ミニドライバーは[*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb)および[*Strminirequesttimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)ルーチンを提供する必要があります。 クラスドライバーは、要求をキャンセルまたはタイムアウトしたときに、それぞれのミニドライバールーチンを呼び出します。

クラスドライバーは、基になる i/o 要求がオペレーティングシステムによって取り消された場合に、要求をキャンセルします。 クラスドライバーは、処理に時間がかかりすぎる要求をタイムアウトさせます。これにより、ストリーム要求ブロックの**Timeoutcounter**メンバー内の要求がタイムアウトするまでの秒数のカウンターが減少します。 ミニドライバーが長時間にわたって要求の処理を遅延させる必要がある場合、 **Timeoutcounter**メンバーを0に設定する必要があります。これにより、クラスドライバーは要求をタイムアウトにしません。 ミニドライバーが要求の処理を再開したら、 **Timeoutcounter**をリセットして、ストリーム要求ブロックの**timeoutcounter**メンバーと同じにする必要があります。 ミニドライバーは、 **Timeoutoriginal**をリセットして、要求がタイムアウトするまでの時間を変更できます。詳細については、「 [**HW\_STREAM\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block) 」を参照してください。

 

 





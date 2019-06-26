---
title: RequestProcessing の規則セット (KMDF)
description: これらの規則を使用すると、ドライバーが正しく完了するか、I/O 要求パケット (IRP) をキャンセルすることを確認します。
ms.assetid: 25162982-6A98-4018-82B3-8DD3E0A0A002
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1827342eaa276ae52419335ebe124161e5821bc9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353876"
---
# <a name="requestprocessing-rule-set-kmdf"></a>RequestProcessing の規則セット (KMDF)


これらの規則を使用すると、ドライバーが正しく完了するか、I/O 要求パケット (IRP) をキャンセルすることを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-changequeuestate.md" data-raw-source="[&lt;strong&gt;ChangeQueueState&lt;/strong&gt;](kmdf-changequeuestate.md)"><strong>ChangeQueueState</strong></a></p></td>
<td align="left"><p><a href="kmdf-changequeuestate.md" data-raw-source="[&lt;strong&gt;ChangeQueueState&lt;/strong&gt;](kmdf-changequeuestate.md)"> <strong>ChangeQueueState</strong> </a>ルールは、WDF ドライバーが同時実行のスレッドから、キューの状態を変更しようとしていないまたは Ddi 1 つずつから内で変更と同じ状態を呼び出さないことを指定します。スレッドです。 キューの状態が変化するコールバック関数は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop" data-raw-source="[&lt;strong&gt;WdfIoQueueStop&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)"> <strong>WdfIoQueueStop</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously)"> <strong>WdfIoQueueStopSynchronously</strong></a>、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge" data-raw-source="[&lt;strong&gt;WdfIoQueuePurge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge)"> <strong>WdfIoQueuePurge</strong></a>、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueuePurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)"><strong>WdfIoQueuePurgeSynchronously</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain" data-raw-source="[&lt;strong&gt;WdfIoQueueDrain&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain)"> <strong>WdfIoQueueDrain</strong> </a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueDrainSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)"> <strong>WdfIoQueueDrainSynchronously</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurge" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurge)"> <strong>WdfIoQueueStopAndPurge</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)"> <strong>WdfIoQueueStopAndPurgeSynchronously</strong></a>します。 キューの状態の変更が既に進行中の場合、これらの Ddi が呼び出された場合、クラッシュや応答しなくなるコンピューターがなります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-completecanceledreq.md" data-raw-source="[&lt;strong&gt;CompleteCanceledReq&lt;/strong&gt;](kmdf-completecanceledreq.md)"><strong>CompleteCanceledReq</strong></a></p></td>
<td align="left"><p><a href="kmdf-completecanceledreq.md" data-raw-source="[&lt;strong&gt;CompleteCanceledReq&lt;/strong&gt;](kmdf-completecanceledreq.md)"> <strong>CompleteCanceledReq</strong> </a>ルールを指定する要求が既に取り消されています、要求が無効、およびドライバーは完了していない場合。 ドライバーには、キャンセル可能なマークされている要求がアクティブ、中に、要求がない既に取り消されたことを確認する必要があります。 ドライバーがこのチェックを行わない場合は、ドライバーは、解放された要求を完了があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](kmdf-doublecompletion.md)"><strong>DoubleCompletion</strong></a></p></td>
<td align="left"><p><a href="kmdf-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](kmdf-doublecompletion.md)"> <strong>DoubleCompletion</strong> </a>ルールでは、ドライバーする必要があります、I/O 要求を 2 回完了していないことを指定します。 同じ要求に 1 行に 2 回、次のメソッドを呼び出すことはできません。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete" data-raw-source="[&lt;strong&gt;WdfRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)"><strong>WdfRequestComplete</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation" data-raw-source="[&lt;strong&gt;WdfRequestCompleteWithInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)"> <strong>WdfRequestCompleteWithInformation</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost" data-raw-source="[&lt;strong&gt;WdfRequestCompleteWithPriorityBoost&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)"> <strong>WdfRequestCompleteWithPriorityBoost</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-doublecompletionlocal.md" data-raw-source="[&lt;strong&gt;DoubleCompletionLocal&lt;/strong&gt;](kmdf-doublecompletionlocal.md)"><strong>DoubleCompletionLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-doublecompletionlocal.md" data-raw-source="[DoubleCompletionLocal](kmdf-doublecompletionlocal.md)">DoubleCompletionLocal</a>ルールでは、ドライバーする必要があります、I/O 要求を 2 回完了していないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtiostopcancel.md" data-raw-source="[&lt;strong&gt;EvtIoStopCancel&lt;/strong&gt;](kmdf-evtiostopcancel.md)"><strong>EvtIoStopCancel</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopcancel.md" data-raw-source="[&lt;strong&gt;EvtIoStopCancel&lt;/strong&gt;](kmdf-evtiostopcancel.md)"> <strong>EvtIoStopCancel</strong> </a>ルールでは、ことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>コールバック関数では、ドライバーを呼び出す次のいずれかI/O 要求が、キャンセル可能な方法です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtiostopcompleteorstopack.md" data-raw-source="[&lt;strong&gt;EvtIoStopCompleteOrStopAck&lt;/strong&gt;](kmdf-evtiostopcompleteorstopack.md)"><strong>EvtIoStopCompleteOrStopAck</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopcompleteorstopack.md" data-raw-source="[&lt;strong&gt;EvtIoStopCompleteOrStopAck&lt;/strong&gt;](kmdf-evtiostopcompleteorstopack.md)"> <strong>EvtIoStopCompleteOrStopAck</strong> </a>ルールでは、ことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>コールバック関数、ドライバーは、1 つを呼び出す、フレームワークによって表示される I/O 要求ごとに次のメソッド。 これを行わないと、ドライバーは別の低電力状態に入るをシステムをブロックする可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtsurpriseremovenosuspendqueue.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoSuspendQueue&lt;/strong&gt;](kmdf-evtsurpriseremovenosuspendqueue.md)"><strong>EvtSurpriseRemoveNoSuspendQueue</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtsurpriseremovenosuspendqueue.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoSuspendQueue&lt;/strong&gt;](kmdf-evtsurpriseremovenosuspendqueue.md)"> <strong>EvtSurpriseRemoveNoSuspendQueue</strong> </a>ルールは、WDF ドライバーの電源べきではないドレインいること、停止、または、キューから削除するを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"> <em>EvtDeviceSurpriseRemoval</em>。</a>コールバック関数では、代わりに自己管理される I/O のコールバック関数を使用する必要があります。 <em>EvtDeviceSurpriseRemoval</em>コールバック関数は、電源のパスと同期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-fileobjectconfigured.md" data-raw-source="[&lt;strong&gt;FileObjectConfigured&lt;/strong&gt;](kmdf-fileobjectconfigured.md)"><strong>FileObjectConfigured</strong></a></p></td>
<td align="left"><p><a href="kmdf-fileobjectconfigured.md" data-raw-source="[&lt;strong&gt;FileObjectConfigured&lt;/strong&gt;](kmdf-fileobjectconfigured.md)"> <strong>FileObjectConfigured</strong> </a>ルールを指定するへの呼び出し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject" data-raw-source="[&lt;strong&gt;WdfRequestGetFileObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject)"> <strong>WdfRequestGetFileObject</strong> </a> への呼び出しでメソッドの前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetFileObjectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)"><strong>WdfDeviceInitSetFileObjectConfig</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-internalioctlreqs.md" data-raw-source="[&lt;strong&gt;InternalIoctlReqs&lt;/strong&gt;](kmdf-internalioctlreqs.md)"><strong>InternalIoctlReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-internalioctlreqs.md" data-raw-source="[&lt;strong&gt;InternalIoctlReqs&lt;/strong&gt;](kmdf-internalioctlreqs.md)"> <strong>InternalIoctlReqs</strong> </a>ルールでは、内部 IOCTL 要求は不適切な KMDF 要求送信デバイス ドライバー インターフェイス (Ddi) に渡されませんしていることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-invalidreqaccess.md" data-raw-source="[&lt;strong&gt;InvalidReqAccess&lt;/strong&gt;](kmdf-invalidreqaccess.md)"><strong>InvalidReqAccess</strong></a></p></td>
<td align="left"><p><a href="kmdf-invalidreqaccess.md" data-raw-source="[&lt;strong&gt;InvalidReqAccess&lt;/strong&gt;](kmdf-invalidreqaccess.md)"> <strong>InvalidReqAccess</strong> </a>ルールでは、要求が完了したか取り消された後にアクセスしていないことを指定します。 このルールが二重の完了をチェックする規則などの他のルールでは、重複するまたは要求をチェックする規則マークされているキャンセル可能な 2 つの時刻。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-invalidreqaccesslocal.md" data-raw-source="[&lt;strong&gt;InvalidReqAccessLocal&lt;/strong&gt;](kmdf-invalidreqaccesslocal.md)"><strong>InvalidReqAccessLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-invalidreqaccesslocal.md" data-raw-source="[&lt;strong&gt;InvalidReqAccessLocal&lt;/strong&gt;](kmdf-invalidreqaccesslocal.md)"> <strong>InvalidReqAccessLocal</strong> </a>ルールが完了したか取り消された後にローカルで作成された要求はアクセスされませんを指定します。 このルールが二重の完了をチェックする規則などの他のルールでは、重複するまたは要求をチェックする規則マークされているキャンセル可能な 2 つの時刻。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-ioctlreqs.md" data-raw-source="[&lt;strong&gt;IoctlReqs&lt;/strong&gt;](kmdf-ioctlreqs.md)"><strong>IoctlReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-ioctlreqs.md" data-raw-source="[&lt;strong&gt;IoctlReqs&lt;/strong&gt;](kmdf-ioctlreqs.md)"> <strong>IoctlReqs</strong> </a>ルールは、IOCTL 要求が不適切な KMDF 要求に渡すことはできないか、デバイス ドライバー インターフェイス (Ddi) を送信することを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-markcanconcancreqlocal.md" data-raw-source="[&lt;strong&gt;MarkCancOnCancReqLocal&lt;/strong&gt;](kmdf-markcanconcancreqlocal.md)"><strong>MarkCancOnCancReqLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-markcanconcancreqlocal.md" data-raw-source="[&lt;strong&gt;MarkCancOnCancReqLocal&lt;/strong&gt;](kmdf-markcanconcancreqlocal.md)"> <strong>MarkCancOnCancReqLocal</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"> <strong>WdfRequestMarkCancelable</strong> </a>メソッドは呼び出せません 2 つの連続します。同じ I/O 要求の時間。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="noioqueuepurgesynchronously.md" data-raw-source="[&lt;strong&gt;NoIoQueuePurgeSynchronously&lt;/strong&gt;](noioqueuepurgesynchronously.md)"><strong>NoIoQueuePurgeSynchronously</strong></a></p></td>
<td align="left"><p><a href="noioqueuepurgesynchronously.md" data-raw-source="[&lt;strong&gt;NoIoQueuePurgeSynchronously&lt;/strong&gt;](noioqueuepurgesynchronously.md)"> <strong>NoIoQueuePurgeSynchronously</strong> </a>ルールでは、WDF のドライバーを呼び出さないことを検証、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously)"> <strong>WdfIoQueueStopSynchronously</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueDrainSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)"><strong>WdfIoQueueDrainSynchronously</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)"> <strong>WdfIoQueueStopAndPurgeSynchronously</strong></a>、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueuePurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)"> <strong>WdfIoQueuePurgeSynchronously</strong> </a>次 EvtIO から functions におけるキュー オブジェクト イベントのコールバック関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-outputbufferapi.md" data-raw-source="[&lt;strong&gt;OutputBufferAPI&lt;/strong&gt;](kmdf-outputbufferapi.md)"><strong>OutputBufferAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-outputbufferapi.md" data-raw-source="[&lt;strong&gt;OutputBufferAPI&lt;/strong&gt;](kmdf-outputbufferapi.md)"> <strong>OutputBufferAPI</strong> </a>ルールでは、バッファー取得のための正しい Ddi で使用されることを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a>コールバック関数。 内で、 <em>EvtIoWrite</em>コールバック関数では、次の Ddi はバッファー取得のため呼び出すことができません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-readreqs.md" data-raw-source="[&lt;strong&gt;ReadReqs&lt;/strong&gt;](kmdf-readreqs.md)"><strong>ReadReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-readreqs.md" data-raw-source="[&lt;strong&gt;ReadReqs&lt;/strong&gt;](kmdf-readreqs.md)"> <strong>ReadReqs</strong> </a>ルールでは、その読み取り要求は、不適切な KMDF メソッドに渡されませんを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqcompletionroutine.md" data-raw-source="[&lt;strong&gt;ReqCompletionRoutine&lt;/strong&gt;](kmdf-reqcompletionroutine.md)"><strong>ReqCompletionRoutine</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqcompletionroutine.md" data-raw-source="[&lt;strong&gt;ReqCompletionRoutine&lt;/strong&gt;](kmdf-reqcompletionroutine.md)"> <strong>ReqCompletionRoutine</strong> </a>ルールでは、要求が I/O のターゲットに送信される前に完了ルーチンを設定する必要がありますを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqdelete.md" data-raw-source="[&lt;strong&gt;ReqDelete&lt;/strong&gt;](kmdf-reqdelete.md)"><strong>ReqDelete</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqdelete.md" data-raw-source="[&lt;strong&gt;ReqDelete&lt;/strong&gt;](kmdf-reqdelete.md)"> <strong>ReqDelete</strong> </a>ルールを指定するドライバーが作成した要求は渡されないという<em>WdfRequestCompleteXxx</em>関数。 代わりに、要求は、完了時に削除する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqiscanconcancreq.md" data-raw-source="[&lt;strong&gt;ReqIsCancOnCancReq&lt;/strong&gt;](kmdf-reqiscanconcancreq.md)"><strong>ReqIsCancOnCancReq</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqiscanconcancreq.md" data-raw-source="[&lt;strong&gt;ReqIsCancOnCancReq&lt;/strong&gt;](kmdf-reqiscanconcancreq.md)"> <strong>ReqIsCancOnCancReq</strong> </a>ルールでは、ことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled" data-raw-source="[&lt;strong&gt;WdfRequestIsCanceled&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)"> <strong>WdfRequestIsCanceled</strong> </a>メソッドはない要求でのみ呼び出すことができますキャンセル可能としてマークされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqmarkcancelablesend.md" data-raw-source="[&lt;strong&gt;ReqMarkCancelableSend&lt;/strong&gt;](kmdf-reqmarkcancelablesend.md)"><strong>ReqMarkCancelableSend</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqmarkcancelablesend.md" data-raw-source="[&lt;strong&gt;ReqMarkCancelableSend&lt;/strong&gt;](kmdf-reqmarkcancelablesend.md)"> <strong>ReqMarkCancelableSend</strong> </a>規則を指定、ドライバーによって転送された要求マークされていないとキャンセル可能な呼び出して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"> <strong>WdfRequestMarkCancelable</strong></a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestcompleted.md" data-raw-source="[&lt;strong&gt;RequestCompleted&lt;/strong&gt;](kmdf-requestcompleted.md)"><strong>RequestCompleted</strong></a></p></td>
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"> <strong>DeferredRequestCompleted</strong> </a>非フィルター ドライバーのドライバーの既定の I/O キューに表示される各要求する必要がありますが完了したこと、要求が遅延または転送、しない限り、規則を指定または場合<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"> <strong>WdfRequestStopAcknowledge</strong> </a>が呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestformattedvalid.md" data-raw-source="[&lt;strong&gt;RequestFormattedValid&lt;/strong&gt;](kmdf-requestformattedvalid.md)"><strong>RequestFormattedValid</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestformattedvalid.md" data-raw-source="[&lt;strong&gt;RequestFormattedValid&lt;/strong&gt;](kmdf-requestformattedvalid.md)"> <strong>RequestFormattedValid</strong> </a>ルールでは、I/O のターゲットに送信する前に、ドライバーは、WDF_REQUEST_SEND_OPTION_SEND_AND_FORGET 要求を除き、すべての要求を書式設定。 を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestgetstatusvalid.md" data-raw-source="[&lt;strong&gt;RequestGetStatusValid&lt;/strong&gt;](kmdf-requestgetstatusvalid.md)"><strong>RequestGetStatusValid</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestgetstatusvalid.md" data-raw-source="[&lt;strong&gt;RequestGetStatusValid&lt;/strong&gt;](kmdf-requestgetstatusvalid.md)"> <strong>RequestGetStatusValid</strong> </a>ことを指定するルール<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetstatus" data-raw-source="[&lt;strong&gt;WdfRequestGetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)"> <strong>WdfRequestGetStatus</strong> </a>のいずれかで要求を呼び出す必要があります、次の場合:</p>
<ul>
<li>ときに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)"> <strong>WdfRequestSend</strong> </a>エラーを返します。</li>
<li>ときに、要求が WDF_REQUEST_SEND_OPTION_SYNCHRONOUS に送信されました。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting.md)"><strong>RequestSendAndForgetNoFormatting</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting.md)"> <strong>RequestSendAndForgetNoFormatting</strong> </a>ルールは、ドライバーが I/O ターゲット WDF_ 送信オプションを使用して I/O ターゲットに送信する前に関数の書式設定を使用して、要求の書式を設定しないことを確認します。REQUEST_SEND_OPTION_SEND_AND_FORGET します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting2.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting2&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting2.md)"><strong>RequestSendAndForgetNoFormatting2</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting2.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting2&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting2.md)"> <strong>RequestSendAndForgetNoFormatting2</strong> </a>ルールは、ドライバーが I/O ターゲット WDF_ 送信オプションを使用して I/O ターゲットに送信する前に関数の書式設定を使用して、要求の書式を設定しないことを確認します。REQUEST_SEND_OPTION_SEND_AND_FORGET します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-stopackwithinevtiostop.md" data-raw-source="[&lt;strong&gt;StopAckWithinEvtIoStop&lt;/strong&gt;](kmdf-stopackwithinevtiostop.md)"><strong>StopAckWithinEvtIoStop</strong></a></p></td>
<td align="left"><p><a href="kmdf-stopackwithinevtiostop.md" data-raw-source="[&lt;strong&gt;StopAckWithinEvtIoStop&lt;/strong&gt;](kmdf-stopackwithinevtiostop.md)"> <strong>StopAckWithinEvtIoStop</strong> </a>ルールでは、ことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"> <strong>WdfRequestStopAcknowledge</strong> </a>関数内からのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>コールバック関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfioqueuefindrequestfailed.md" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequestFailed&lt;/strong&gt;](kmdf-wdfioqueuefindrequestfailed.md)"><strong>WdfIoQueueFindRequestFailed</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueuefindrequestfailed.md" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequestFailed&lt;/strong&gt;](kmdf-wdfioqueuefindrequestfailed.md)"> <strong>WdfIoQueueFindRequestFailed</strong> </a>ルールを指定する<a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"> <strong>WdfIoQueueRetrieveFoundRequest</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference" data-raw-source="[&lt;strong&gt;WdfObjectDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)"> <strong>WdfObjectDereference</strong> </a>後に呼び出す必要がありますのみ<strong>WdfIoQueueFindRequestFailed</strong> STATUS_SUCCESS を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"><strong>WdfIoQueueRetrieveFoundRequest</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"> <strong>WdfIoQueueRetrieveFoundRequest</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)"> <strong>WdfIoQueueRetrieveFoundRequest</strong> </a>メソッドは後でのみ呼び出されます<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)"> <strong>WdfIoQueueFindRequest</strong> </a>呼び出され、返される STATUS_SUCCESS および no <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference" data-raw-source="[&lt;strong&gt;WdfObjectDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)"> <strong>WdfObjectDereference</strong> </a>で呼び出されます同じ要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfioqueueretrievenextrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievenextrequest.md)"><strong>WdfIoQueueRetrieveNextRequest</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueueretrievenextrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievenextrequest.md)"> <strong>WdfIoQueueRetrieveNextRequest</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievenextrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)"> <strong>WdfIoQueueRetrieveNextRequest</strong> </a> 後は呼び出されません<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)"><strong>WdfIoQueueFindRequest</strong> </a>が呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-writereqs.md" data-raw-source="[&lt;strong&gt;WriteReqs&lt;/strong&gt;](kmdf-writereqs.md)"><strong>WriteReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-writereqs.md" data-raw-source="[&lt;strong&gt;WriteReqs&lt;/strong&gt;](kmdf-writereqs.md)"> <strong>WriteReqs</strong> </a>ルールでは、書き込み要求が不適切な KMDF メソッドに渡されないことを指定します。</p></td>
</tr>
</tbody>
</table>

 

**RequestProcessing ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **RequestProcessing**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **RequestProcessing.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:RequestProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 






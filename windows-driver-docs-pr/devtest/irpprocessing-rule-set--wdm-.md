---
title: IrpProcessing の規則セット (WDM)
description: これらの規則を使用すると、ドライバーが I/O 要求パケット (IRP) を正しく処理することを確認します。
ms.assetid: C11F1FD7-DA41-4A72-A0EB-97C1D79ECC21
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 06a4dfc4288edcbba7edeeec90b4c6fdc2f2329d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373684"
---
# <a name="irpprocessing-rule-set-wdm"></a>IrpProcessing の規則セット (WDM)


これらの規則を使用すると、ドライバーが I/O 要求パケット (IRP) を正しく処理することを確認します。

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
<td align="left"><p><a href="wdm-completerequest.md" data-raw-source="[&lt;strong&gt;CompleteRequest&lt;/strong&gt;](wdm-completerequest.md)"><strong>CompleteRequest</strong></a></p></td>
<td align="left"><p><a href="wdm-completerequest.md" data-raw-source="[&lt;strong&gt;CompleteRequest&lt;/strong&gt;](wdm-completerequest.md)"> <strong>CompleteRequest</strong> </a>ルールを確認、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>完了ルーチンの実行後に、ルーチンが呼び出されないとある STATUS_MORE_PROCESSING_REQUIRED は返されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"><strong>CompleteRequestStatusCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"> <strong>CompleteRequestStatusCheck</strong> </a> IRP の I/O の状態値が下位のドライバーによって返される状態値と一致する規則を確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"><strong>CompletionRoutineRegistered</strong></a></p></td>
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"> <strong>CompletionRoutineRegistered</strong> </a>規則で指定された場合、ディスパッチ ルーチンのレジスタを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;strong&gt;IoCompletion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <strong>IoCompletion</strong> </a>ルーチンを使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong></a>、ディスパッチ ルーチンを呼び出す必要がありますそれ以降<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"><strong>保留</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](wdm-doublecompletion.md)"><strong>DoubleCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion (WDM)&lt;/strong&gt;](wdm-doublecompletion.md)"> <strong>DoubleCompletion (WDM)</strong> </a>ルールでは、ドライバーを呼び出してはならないことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>同じ 2 回のルーチンIRP します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"> <strong>IoReuseIrp</strong> </a>ルールでは、ドライバーを使用することを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp)"> <strong>IoReuseIrp</strong> </a> に以前割り当てられたIrpでのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"><strong>IoReuseIrp2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"> <strong>IoReuseIrp2</strong> </a>ルールでは、ドライバーを使用することを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp)"> <strong>IoReuseIrp</strong> </a>内で割り当てられていた Irp でのみ、ドライバー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"><strong>IoSetCompletionExCompleteIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"> <strong>IoSetCompletionExCompleteIrp</strong> </a>ルールでは、ことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong> </a>ルーチンには、NTSTATUS 値が返されます. ドライバーを確認するには、この値を確認する必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <em>IoCompletion</em> </a>ルーチンは、呼び出す前に正常に登録されました<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"><strong>保留</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>場合<strong>IoSetCompletionRoutineEx</strong>が失敗した IRP を完了する必要があり、ディスパッチ ルーチンを返す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"><strong>IoSetCompletionRoutineExCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"> <strong>IoSetCompletionRoutineExCheck</strong> </a>ルールでは、ことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong> </a>ルーチンは、NTSTATUS を返します値。 ドライバーを確認するには、この値を確認する必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <em>IoCompletion</em> </a>ルーチンは、呼び出す前に正常に登録されました<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"><strong>保留</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"><strong>IoSetCompletionRoutineExCheckDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"> <strong>IoSetCompletionRoutineExCheckDeviceObject</strong> </a>ルールを指定するには、現在のデバイス オブジェクトが渡されない場合<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong></a>と下位のデバイス オブジェクトが、これにより、競合状態、現在のデバイス オブジェクトできません読み込まれた完了ルーチンが実行されていない場合でもです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"><strong>IoSetCompletionRoutineNonPnpDriver</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"> <strong>IoSetCompletionRoutineNonPnpDriver</strong> </a>ルールでは、PnP ドライバーではないドライバーを使用することを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong> </a>いない<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)"> <strong>IoSetCompletionRoutine</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"><strong>IrpCancelField</strong></a></p></td>
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"> <strong>IrpCancelField</strong> </a>ルールでは、ドライバーがの値を確認するように指定します、 <strong>Irp -&gt;キャンセル</strong>メンバー IRP のキャンセル ルーチンを設定するときに保留します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"><strong>IrpProcessingComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"> <strong>IrpProcessingComplete</strong> </a>ルールでは、ディスパッチ ルーチン STATUS_SUCCESS を返す場合 IRP する必要がありますが完了しているか、ドライバー自体または下位のドライバーを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"><strong>LowerDriverReturn</strong></a></p></td>
<td align="left"><p><a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"> <strong>LowerDriverReturn</strong> </a>ルールでは、その後の使用を指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>保留</strong></a>下位のドライバーを呼び出すには、ドライバーが呼び出しから戻り値の状態を保存し、ディスパッチ ルーチンに受信した戻り値の状態を渡します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"><strong>SignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"> <strong>SignalEventInCompletion</strong> </a>ルールでは、非同期の IRP を処理するときに呼び出す ドライバーが必要なを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>完了ルーチンの場合、 <strong>Irp の&gt;PendingReturned</strong>フラグを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"><strong>SignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"> <strong>SignalEventInCompletion2</strong> </a>ルールでは、非同期の IRP を処理するときに呼び出す ドライバーが必要なを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>完了ルーチンの場合、 <strong>Irp の&gt;PendingReturned</strong>フラグを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"><strong>SignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"> <strong>SignalEventInCompletion3</strong> </a>ルールでは、非同期の IRP を処理するときに呼び出す ドライバーが必要なを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>完了ルーチンの場合、 <strong>Irp の&gt;PendingReturned</strong>フラグを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"><strong>StartIoCancel</strong></a></p></td>
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"> <strong>StartIoCancel</strong> </a>ルールでは、ドライバーを呼び出してはならないことを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes)"> <strong>IoSetStartIoAttributes</strong> </a>で、 <em>オブジェクト</em>パラメーターに設定<strong>FALSE</strong>呼び出す前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine" data-raw-source="[&lt;strong&gt;IoSetCancelRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)"> <strong>IoSetCancelRoutine</strong> </a>以外<strong>NULL</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel" data-raw-source="[&lt;strong&gt;Cancel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)"><strong>キャンセル</strong></a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"><strong>StartIoRecursion</strong></a></p></td>
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"> <strong>StartIoRecursion</strong> </a>規則で指定された場合、ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio" data-raw-source="[&lt;strong&gt;StartIo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)"> <strong>StartIo</strong> </a>ルーチンにはへの呼び出しが含まれています<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)"> <strong>います</strong></a>、ドライバーは呼び出す必要がありますまず<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes)"> <strong>IoSetStartIoAttributes</strong> </a>で、 <em>DeferredStartIo</em>属性に設定<strong>TRUE</strong>します。 それ以外の場合、無限再帰が発生することができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"><strong>PnpRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"> <strong>PnpRemove</strong> </a>ルールでは、ドライバーが IRP_MN_SURPRISE_REMOVAL、IRP_MN_CANCEL_REMOVE_DEVICE、IRP_MN_CANCEL_STOP_DEVICE、または IRP_MN_REMOVE_DEVICE 要求を完了できないことを指定します、失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"><strong>PnpSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"> <strong>PnpSurpriseRemove</strong> </a>ルールを指定するドライバーは呼び出しません IoDeleteDevice または IoDetachDevice 処理中に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)"> <strong>IRP_MN_SURPRISE_REMOVAL</strong></a>要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"><strong>PowerDownAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"> <strong>PowerDownAllocate</strong> </a>ルールでは、エントリの IRP_MN_SET_POWER 要求を処理するときに、ドライバーを FDO して FIDO はメモリが割り当てられませんを指定します、 <strong>SystemPowerState</strong>移行 [S1 に s0 から移動します。S5]。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"><strong>PowerDownFail</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"> <strong>PowerDownFail</strong> </a>ルールでは、エントリのデバイスの電源を切ったとき、FDO または FIDO ドライバーする必要があります、IRP_MN_SET_POWER 要求が失敗しないを指定します。 このルールは、FDO および FIDO ドライバーのみに適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"><strong>PowerIrpDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"> <strong>PowerIrpDDIs</strong> </a>ルールでは、システムまたはデバイス IRP_MN_SET_POWER に対し、IRP_MJ_POWER、ドライバーが処理する場合は PASSIVE_LEVEL の呼び出しであることができますのみ Ddi を呼び出すことことがない必要がありますを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerupfail.md" data-raw-source="[&lt;strong&gt;PowerUpFail&lt;/strong&gt;](wdm-powerupfail.md)"><strong>PowerUpFail</strong></a></p></td>
<td align="left"><p>PowerUpFail ルールでは、ユーザーがデバイスの電源を入れるときは、FDO または FIDO ドライバーには IRP_MN_SET_POWER 要求は失敗しませんを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"><strong>PnpIrpCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"> <strong>PnpIrpCompletion</strong> </a>ルールは、FDO ドライバーが下位のドライバーを PnP Irp を渡すことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"><strong>WmiComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"> <strong>WmiComplete</strong> </a>ルール指定を処理するときに、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)"> <strong>WMI マイナー IRP</strong></a>、ドライバー呼び出し<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>から戻る前に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchSystemControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <strong>DispatchSystemControl</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"><strong>WmiForward</strong></a></p></td>
<td align="left"><p><a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"> <strong>WmiForward</strong> </a>ルールでは、ドライバーを転送する必要がありますを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRPs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)"> <strong>WMI マイナー Irp</strong> </a>転送が必要な場合。</p></td>
</tr>
</tbody>
</table>

 

**IrpProcessing ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **IrpProcessing**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **IrpProcessing.sdv**で、 **/check**オプション。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 






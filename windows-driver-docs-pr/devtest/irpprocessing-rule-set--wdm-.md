---
title: IrpProcessing の規則セット (WDM)
description: これらのルールを使用して、ドライバーが i/o 要求パケット (IRP) を正しく処理していることを確認します。
ms.assetid: C11F1FD7-DA41-4A72-A0EB-97C1D79ECC21
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 140e82bbb810156649c69ef115c0f9d277dea9d2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840255"
---
# <a name="irpprocessing-rule-set-wdm"></a>IrpProcessing の規則セット (WDM)


これらのルールを使用して、ドライバーが i/o 要求パケット (IRP) を正しく処理していることを確認します。

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
<td align="left"><p><a href="wdm-completerequest.md" data-raw-source="[&lt;strong&gt;CompleteRequest&lt;/strong&gt;](wdm-completerequest.md)"><strong>CompleteRequest</strong></a>ルールは、完了ルーチンの実行後に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>ルーチンが呼び出されず、STATUS_MORE_PROCESSING_REQUIRED を返さないことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"><strong>CompleteRequestStatusCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"><strong>CompleteRequestStatusCheck</strong></a>ルールは、IRP 内の i/o 状態値が、下位ドライバーによって返された状態値と一致することを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"><strong>CompletionRoutineRegistered</strong></a></p></td>
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"><strong>CompletionRoutineRegistered</strong></a>ルールは、ディスパッチルーチンが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a>を使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;strong&gt;IoCompletion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><strong>iocompletion</strong></a>ルーチンを登録する場合、ディスパッチルーチンが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>を呼び出す必要があることを指定します。PoCallDriver</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](wdm-doublecompletion.md)"><strong>DoubleCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion (WDM)&lt;/strong&gt;](wdm-doublecompletion.md)"><strong>DoubleCompletion (WDM)</strong></a>規則は、同じ IRP に対してドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>ルーチンを2回呼び出すことができないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"><strong>IoReuseIrp</strong></a>規則は、ドライバーが以前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>Ioallocateirp</strong></a>で割り当てられた irp でのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)"><strong>IoReuseIrp</strong></a>を使用するように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"><strong>IoReuseIrp2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"><strong>IoReuseIrp2</strong></a>規則は、ドライバーが、ドライバー内で以前に割り当てられた irp でのみ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)"><strong>IoReuseIrp</strong></a>を使用することを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"><strong>IoSetCompletionExCompleteIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"><strong>IoSetCompletionExCompleteIrp</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IOSETCOMPLETIONROUTINEEX</strong></a>ルーチンが NTSTATUS 値を返すことを指定します。 ドライバーは、この値をチェックして、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を呼び出す前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>iocompletion</em></a>ルーチンが正常に登録されたかどうかを確認し、 <strong>IOSETCOMPLETIONROUTINEEX</strong>が失敗した場合は IRP を完了する必要があります。ディスパッチルーチンはを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"><strong>IoSetCompletionRoutineExCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"><strong>IoSetCompletionRoutineExCheck</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IOSETCOMPLETIONROUTINEEX</strong></a>ルーチンが NTSTATUS 値を返すことを指定します。 ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を呼び出す前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>iocompletion</em></a>ルーチンが正常に登録されたかどうかを確認するために、この値を確認する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"><strong>IoSetCompletionRoutineExCheckDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"><strong>IoSetCompletionRoutineExCheckDeviceObject</strong></a>ルールでは、現在のデバイスオブジェクトが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a>に渡されず、それより小さいデバイスオブジェクトがである場合に、現在のデバイスオブジェクトが次のような競合状態になる可能性があることを指定します。完了ルーチンが実行されていない場合でも、アンロードされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"><strong>IoSetCompletionRoutineNonPnpDriver</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"><strong>IoSetCompletionRoutineNonPnpDriver</strong></a>ルールは、PnP ドライバー以外のドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a> Not <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)"><strong>ioset ルーチン</strong></a>を使用する必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"><strong>IrpCancelField</strong></a></p></td>
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"><strong>Irpcancelfield</strong></a>ルールでは、保留中の irp に対してキャンセルルーチンを設定するときに、ドライバーが<strong>Irp-&gt;cancel</strong>メンバーの値をチェックするように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"><strong>IrpProcessingComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"><strong>Irpprocessingcomplete</strong></a>ルールでは、ディスパッチルーチンから STATUS_SUCCESS が返される場合、IRP はドライバー自体または下位レベルのドライバーによって完了されている必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"><strong>ドライバーのダウンリターン</strong></a></p></td>
<td align="left"><p>Lower <a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"><strong>Driverreturn</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>を使用して下位のドライバーを呼び出すと、ドライバーが呼び出しから戻りステータスを保存し、受信したリターンステータスをディスパッチルーチンに渡すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"><strong>SignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"><strong>Signaleventincompletion</strong></a>ルールは、非同期の irp を処理するときに、 <strong>Irp&gt;pendingreturned</strong>フラグが設定されている場合に、ドライバーが完了ルーチンで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"><strong>SignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"><strong>SignalEventInCompletion2</strong></a>規則は、非同期の irp を処理するときに、 <strong>Irp-&gt;pendingreturned</strong>フラグが設定されている場合に、ドライバーが完了ルーチンの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"><strong>SignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"><strong>SignalEventInCompletion3</strong></a>規則は、非同期の irp を処理するときに、 <strong>Irp-&gt;pendingreturned</strong>フラグが設定されている場合に、ドライバーが完了ルーチンの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"><strong>StartIoCancel</strong></a></p></td>
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"><strong>Startiocancel</strong></a> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine" data-raw-source="[&lt;strong&gt;IoSetCancelRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)"><strong>ルールでは</strong></a><strong>、非</strong>キャンセルパラメーターを<strong>FALSE</strong>に<em>設定して</em>、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)"><strong>iosetstartioattributes</strong></a>を呼び出してはいけないことを指定します。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel" data-raw-source="[&lt;strong&gt;Cancel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)"></a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"><strong>StartIoRecursion</strong></a></p></td>
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"><strong>StartIoRecursion</strong></a>ルールでは、ドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio" data-raw-source="[&lt;strong&gt;StartIo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)"><strong>StartIo</strong></a>ルーチンに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)"><strong>iostartnextpacket</strong></a>の呼び出しが含まれている場合、ドライバーは最初に<em>DeferredStartIo</em>属性をに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)"></a> <strong>設定して iosetstartioattributes を呼び出す必要があることを指定します。TRUE</strong>。 それ以外の場合、無限再帰が発生する可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"><strong>PnpRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"><strong>PnpRemove</strong></a>ルールでは、ドライバーが IRP_MN_SURPRISE_REMOVAL、IRP_MN_CANCEL_REMOVE_DEVICE、IRP_MN_CANCEL_STOP_DEVICE、または IRP_MN_REMOVE_DEVICE 要求を失敗として完了できないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"><strong>PnpSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"><strong>PnpSurpriseRemove</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a>要求の処理中に、ドライバーが Iodeletedevice または IoDetachDevice を呼び出さないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"><strong>PowerDownAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"><strong>Powerdownallocate</strong></a>ルールでは、s0 から [S1... に向かう<strong>SYSTEMPOWERSTATE</strong>遷移の IRP_MN_SET_POWER 要求を処理するときに、FDO および FIDO ドライバーがメモリを割り当てないことを指定します。S5]。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"><strong>PowerDownFail</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"><strong>Powerdownfail</strong></a>ルールでは、デバイスの電源が入っているときに、FDO または FIDO ドライバーが IRP_MN_SET_POWER 要求に失敗しないように指定します。 このルールは、FDO および FIDO ドライバーにのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"><strong>PowerIrpDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"><strong>Powerirpddis</strong></a>ルールでは、ドライバーがシステムまたは IRP_MN_SET_POWER を使用したデバイスの処理を処理するときに、PASSIVE_LEVEL でのみ呼び出すことができる DDIs を呼び出さないように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerupfail.md" data-raw-source="[&lt;strong&gt;PowerUpFail&lt;/strong&gt;](wdm-powerupfail.md)"><strong>PowerUpFail</strong></a></p></td>
<td align="left"><p>PowerUpFail ルールでは、デバイスの電源が入っているときに、FDO または FIDO ドライバーが IRP_MN_SET_POWER 要求に失敗しないように指定しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"><strong>PnpIrpCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"><strong>PnpIrpCompletion</strong></a>ルールは、FDO ドライバーが PnP irp を下位ドライバーに渡すことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"><strong>WmiComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"><strong>WmiComplete</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)"><strong>WMI のマイナー IRP</strong></a>を処理するときに、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>を呼び出してから、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchSystemControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><strong>DispatchSystemControl</strong></a>ルーチンから制御を戻すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"><strong>参照先</strong></a></p></td>
<td align="left"><p>"Wmi<a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"><strong>転送</strong></a>" 規則は、転送が必要な場合に、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRPs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)"><strong>WMI のマイナー irp</strong></a>を転送する必要があることを指定します。</p></td>
</tr>
</tbody>
</table>

 

**IrpProcessing 規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[irpprocessing]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**irpprocessing. sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 






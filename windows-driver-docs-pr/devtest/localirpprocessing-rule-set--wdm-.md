---
title: LocalIrpProcessing の規則セット (WDM)
description: ドライバーによって作成された i/o 要求パケット (IRP) が正しく処理されることを確認するには、これらの規則を使用します。
ms.assetid: 2D10086F-4FCB-4BB1-AF63-49625DCA1A44
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6656bef347051b16f697a011c602b5da5c878eb1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839416"
---
# <a name="localirpprocessing-rule-set-wdm"></a>LocalIrpProcessing の規則セット (WDM)


ドライバーによって作成された i/o 要求パケット (IRP) が正しく処理されることを確認するには、これらの規則を使用します。

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
<td align="left"><p><a href="wdm-ioallocatecomplete.md" data-raw-source="[&lt;strong&gt;IoAllocateComplete&lt;/strong&gt;](wdm-ioallocatecomplete.md)"><strong>IoAllocateComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocatecomplete.md" data-raw-source="[&lt;strong&gt;IoAllocateComplete&lt;/strong&gt;](wdm-ioallocatecomplete.md)"><strong>IoAllocateComplete</strong></a>規則は、IRP が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>Ioallocateirp</strong></a>で作成された場合に、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>を呼び出さないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"><strong>IoAllocateFree</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"><strong>Ioallocatefree</strong></a>ルールは、以前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>ioallocateirp</strong></a>で割り当てられた irp でのみ、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>iofreeirp</strong></a>を使用する必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"><strong>IoAllocateForward</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"><strong>Ioallocateforward</strong></a>ルールは、IRP が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>Ioallocateirp</strong></a>の呼び出しによって生成される場合、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を呼び出す前に、ドライバーが完了ルーチンを設定する必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"><strong>Ioallocateirpq Signaleventincompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"><strong>IoallocateiKeSetEvent Signaleventincompletion</strong></a>規則は、 <strong>Irp-&gt;pendingreturned</strong>フラグが設定され、完了ルーチンがローカルでを処理するときに、完了ルーチンで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"></a>を呼び出す必要があることを指定します。非同期 IRP を作成しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"><strong>IoAllocateIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"><strong>IoAllocateIrpSignalEventInCompletion2</strong></a>ルールでは、 <strong>Irp&gt;pendingreturned</strong>フラグが設定され、完了ルーチンがローカルに作成されたを処理するときに、完了ルーチンで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。非同期の IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"><strong>IoAllocateIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"><strong>IoAllocateIrpSignalEventInCompletion3</strong></a>ルールでは、 <strong>Irp&gt;pendingreturned</strong>フラグが設定され、完了ルーチンがローカルに作成されたを処理するときに、完了ルーチンで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。非同期の IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"><strong>Ioallocateirpq Signaleventinを Timeout</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"><strong>Ioallocateirpq Signaleventincompletion</strong></a>ルールは、IRP のイベントが完了ルーチンで通知される必要があるため、低いドライバーがを返すまで、このドライバーが無期限に待機することを検出した場合に、欠陥を報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"><strong>IoBuildDeviceControlNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"><strong>IoBuildDeviceControlNoFree</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>IoBuildDeviceIoControlRequest</strong></a>を呼び出すドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>iofreeirp</strong></a>を呼び出すことができないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"><strong>IoBuildDeviceControlWait</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>POCALLDRIVER</strong></a>がありますを返す場合、 <a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"><strong>IoBuildDeviceControlWait</strong></a>規則は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a>ルーチンを呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"><strong>IoBuildDeviceControlWaitTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"><strong>IoBuildDeviceControlWaitTimeout</strong></a>ルールは、IRP のイベントが完了ルーチンで通知される必要があるため、下位のドライバーがを返すまで、このドライバーが無期限に待機することを検出した場合に、欠陥を報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"><strong>IoBuildDeviceIoControlSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"><strong>IoBuildDeviceIoControlSetEvent</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>IoBuildDeviceIoControlRequest</strong></a>を呼び出すドライバーが、呼び出し元が割り当てられ初期化されたイベントオブジェクトへのポインターを提供する場合、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出すことができないように指定します。 <strong>KeSetEvent</strong>は、この IRP のドライバーによって呼び出される必要はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"><strong>IoBuildFsdComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"><strong>IoBuildFsdComplete</strong></a>規則は、IRP が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>を使用して作成された場合に、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>を呼び出さないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"><strong>IoBuildFsdForward</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"><strong>IoBuildFsdForward</strong></a>規則は、IRP が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>の呼び出しによって生成される場合に、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>を呼び出す前に、完了ルーチンを設定する必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"><strong>IoBuildFsdFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"><strong>IoBuildFsdFree</strong></a>規則は、以前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>で割り当てられた irp でのみ、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>iofreeirp</strong></a>を使用するように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"><strong>IoBuildFsdIrpSignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"><strong>Iobuildfsdirpsignaleventincompletion</strong></a>規則は、 <strong>Irp&gt;pendingreturned</strong>フラグが設定され、完了ルーチンがローカルを処理するときに、ドライバーが完了ルーチンで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。非同期 IRP を作成しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"><strong>IoBuildFsdIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"><strong>IoBuildFsdIrpSignalEventInCompletion2</strong></a>ルールでは、 <strong>Irp&gt;pendingreturned</strong>フラグが設定され、完了ルーチンがローカルに作成されたを処理するときに、完了ルーチンで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。非同期の IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"><strong>IoBuildFsdIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"><strong>IoBuildFsdIrpSignalEventInCompletion3</strong></a>ルールでは、 <strong>Irp&gt;pendingreturned</strong>フラグが設定され、完了ルーチンがローカルに作成されたを処理するときに、完了ルーチンで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a>を呼び出す必要があることを指定します。非同期の IRP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"><strong>Iobuildfsdirpsignaleventinによるタイムアウト</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"><strong>Iobuildfsdirpsignaleventincompletion タイムアウト</strong></a>規則は、ドライバーが、低いドライバーがを返すまで無制限に待機する場合に、IRP のイベントが完了ルーチンで通知される必要があるため、障害を報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"><strong>IoBuildSynchronousFsdRequestNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"><strong>IoBuildSynchronousFsdRequestNoFree</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)"><strong>IoBuildSynchronousFsdRequest</strong></a>を呼び出すドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>iofreeirp</strong></a>を呼び出すことができないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"><strong>IoBuildSynchronousFsdRequestWait</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"><strong>IoBuildSynchronousFsdRequestWait</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>pocalldriver</strong></a>がありますを返す場合に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a>を呼び出すように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"><strong>IoBuildSynchronousFsdRequestWaitTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"><strong>IoBuildSynchronousFsdRequestWaitTimeout</strong></a>ルールは、IRP のイベントが完了ルーチンで通知される必要があるため、下位のドライバーがを返すまで、このドライバーが無期限に待機することを検出した場合に、欠陥を報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"><strong>RequestedPowerIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"><strong>Requestedpowerirp</strong></a>ルールは、<code>*Irp</code> ポインター変数を<strong>NULL</strong>に設定して、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)"><strong>PoRequestPowerIrp</strong></a>を呼び出すことを指定します。</p></td>
</tr>
</tbody>
</table>

 

**LocalIrpProcessing 規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[Localirpprocessing]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**Localirpprocessing. sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:LocalIrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 






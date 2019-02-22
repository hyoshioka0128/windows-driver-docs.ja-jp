---
title: LocalIrpProcessing ルール セット (WDM)
description: これらの規則を使用すると、ドライバーがドライバーによって作成される I/O 要求パケット (IRP) を正しく処理することを確認します。
ms.assetid: 2D10086F-4FCB-4BB1-AF63-49625DCA1A44
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: faee2edd659b588a7cc202d6dc2bb355fba2cc9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536838"
---
# <a name="localirpprocessing-rule-set-wdm"></a>LocalIrpProcessing ルール セット (WDM)


これらの規則を使用すると、ドライバーがドライバーによって作成される I/O 要求パケット (IRP) を正しく処理することを確認します。

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
<td align="left"><p><a href="wdm-ioallocatecomplete.md" data-raw-source="[&lt;strong&gt;IoAllocateComplete&lt;/strong&gt;](wdm-ioallocatecomplete.md)"> <strong>IoAllocateComplete</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong> </a> IRP がで作成された場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff548257" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548257)"><strong>IoAllocateIrp</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"><strong>IoAllocateFree</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"> <strong>IoAllocateFree</strong> </a>ルールでは、ドライバーを使用することを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff549113" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549113)"> <strong>IoFreeIrp</strong> </a> Irp で割り振られた以前でのみ<a href="https://msdn.microsoft.com/library/windows/hardware/ff548257" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548257)"> <strong>IoAllocateIrp</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"><strong>IoAllocateForward</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"> <strong>IoAllocateForward</strong> </a> IRP がへの呼び出しによって生成される場合をルール指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff548257" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548257)"> <strong>IoAllocateIrp</strong></a>ドライバーを設定する必要があります、呼び出しの前に完了ルーチン<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"> <strong>PoCallDriver</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"><strong>IoAllocateIrpSignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"> <strong>IoAllocateIrpSignalEventInCompletion</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>が完了するまでルーチンときに、 <strong>Irp -&gt;PendingReturned</strong>フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"><strong>IoAllocateIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"> <strong>IoAllocateIrpSignalEventInCompletion2</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>完了ルーチンで呼び出される必要がありますときに、 <strong>Irp -&gt;PendingReturned</strong>フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"><strong>IoAllocateIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"> <strong>IoAllocateIrpSignalEventInCompletion3</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>完了ルーチンで呼び出される必要がありますときに、 <strong>Irp -&gt;PendingReturned</strong>フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"><strong>IoAllocateIrpSignalEventInCompletionTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"> <strong>IoAllocateIrpSignalEventInCompletionTimeout</strong> </a>ルールは、このドライバーは下まで無期限に待機されていることを検出した場合、問題を報告する IRP のイベントが必要なドライバーが返されます完了ルーチンで通知します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"><strong>IoBuildDeviceControlNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"> <strong>IoBuildDeviceControlNoFree</strong> </a>ルールの呼び出しをドライバーを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548318" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548318)"> <strong>IoBuildDeviceIoControlRequest</strong> </a>を呼び出さないでください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff549113" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549113)"> <strong>IoFreeIrp</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"><strong>IoBuildDeviceControlWait</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"> <strong>IoBuildDeviceControlWait</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553350" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553350)"> <strong>kewaitforsingleobject の 1</strong> </a>場合、ルーチンを呼び出す必要がある<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"> <strong>PoCallDriver</strong> </a> STATUS_PENDING を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"><strong>IoBuildDeviceControlWaitTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"> <strong>IoBuildDeviceControlWaitTimeout</strong> </a>ルールは、このドライバーは下まで無期限に待機されていることを検出した場合、問題を報告 IRP のイベントがシグナル状態になるに必要なドライバーが返されます、メモリを割り当てます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"><strong>IoBuildDeviceIoControlSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"> <strong>IoBuildDeviceIoControlSetEvent</strong> </a>ルールの呼び出しをドライバーを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548318" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548318)"> <strong>IoBuildDeviceIoControlRequest</strong> </a>は許可されません呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>ドライバーは、呼び出し元が割り当てたで初期化イベント オブジェクトへのポインターを提供します。 <strong>KeSetEvent</strong>この IRP のドライバーによって呼び出される必要はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"><strong>IoBuildFsdComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"> <strong>IoBuildFsdComplete</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong> </a> IRP がで作成された場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff548310" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548310)"><strong>IoBuildAsynchronousFsdRequest</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"><strong>IoBuildFsdForward</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"> <strong>IoBuildFsdForward</strong> </a>ルールでは、ドライバーを呼び出す前に完了ルーチンを設定する必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"><strong>PoCallDriver</strong> </a> IRP がへの呼び出しによって生成される場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff548310" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548310)"> <strong>IoBuildAsynchronousFsdRequest</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"><strong>IoBuildFsdFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"> <strong>IoBuildFsdFree</strong> </a>ルールでは、ドライバーを使用することを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff549113" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549113)"> <strong>IoFreeIrp</strong> </a> に以前割り当てられたIrpでのみ<a href="https://msdn.microsoft.com/library/windows/hardware/ff548310" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548310)"><strong>IoBuildAsynchronousFsdRequest</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"><strong>IoBuildFsdIrpSignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"> <strong>IoBuildFsdIrpSignalEventInCompletion</strong> </a>ルールでは、ドライバーを呼び出す必要がありますを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>が完了するまでルーチンときに、 <strong>Irp -&gt;PendingReturned</strong>フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"><strong>IoBuildFsdIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"> <strong>IoBuildFsdIrpSignalEventInCompletion2</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>完了ルーチンで呼び出される必要がありますときに、 <strong>Irp -&gt;PendingReturned</strong>フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"><strong>IoBuildFsdIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"> <strong>IoBuildFsdIrpSignalEventInCompletion3</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"> <strong>KeSetEvent</strong> </a>完了ルーチンで呼び出される必要がありますときに、 <strong>Irp -&gt;PendingReturned</strong>フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"><strong>IoBuildFsdIrpSignalEventInCompletionTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"> <strong>IoBuildFsdIrpSignalEventInCompletionTimeout</strong> </a>ルールは、ドライバーが下まで無期限に待機する場合に、欠陥を報告 IRP のイベントがシグナル状態になるに必要なドライバーが返されます、メモリを割り当てます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"><strong>IoBuildSynchronousFsdRequestNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"> <strong>IoBuildSynchronousFsdRequestNoFree</strong> </a>ルールの呼び出しをドライバーを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff548330" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548330)"> <strong>IoBuildSynchronousFsdRequest</strong> </a>する必要があります呼び出さない<a href="https://msdn.microsoft.com/library/windows/hardware/ff549113" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549113)"> <strong>IoFreeIrp</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"><strong>IoBuildSynchronousFsdRequestWait</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"> <strong>IoBuildSynchronousFsdRequestWait</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff553350" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553350)"> <strong>kewaitforsingleobject の 1</strong> </a>場合に呼び出す必要がありますが<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff559654" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559654)"> <strong>PoCallDriver</strong> </a> STATUS_PENDING を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"><strong>IoBuildSynchronousFsdRequestWaitTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"> <strong>IoBuildSynchronousFsdRequestWaitTimeout</strong> </a>ルールは、このドライバーは下まで無期限に待機されていることを検出した場合、問題を報告 IRP のイベントがシグナル状態になる必要なドライバーが返されますでメモリを割り当てます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"><strong>RequestedPowerIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"> <strong>RequestedPowerIrp</strong> </a>ルールでは、そのドライバーは呼び出しを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff559734" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559734)"> <strong>PoRequestPowerIrp</strong> </a>で、<code>*Irp</code>ポインター変数設定<strong>NULL</strong>します。</p></td>
</tr>
</tbody>
</table>

 

**LocalIrpProcessing ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **LocalIrpProcessing**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **LocalIrpProcessing.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:LocalIrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 






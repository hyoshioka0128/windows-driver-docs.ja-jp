---
title: DDI 使用の規則セット (KMDF)
description: これらのルールを使用して、ドライバーが KMDF DDIs を正しく使用していることを確認します。
ms.assetid: 0A3A012C-A1BB-43A5-B38D-4E98928D07E5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: cbe4fb2bc42ac70c26f5c610603be44b3c32d3da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840291"
---
# <a name="ddi-usage-rule-set-kmdf"></a>DDI 使用の規則セット (KMDF)


これらのルールを使用して、ドライバーが KMDF DDIs を正しく使用していることを確認します。

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
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"><strong>BufAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedioctl.md)"><strong>BufAfterReqCompletedIoctl</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>Evtiodevicecontrol</em></a>コールバック関数内で i/o 要求の完了後に取得される i/o 要求バッファーにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"><strong>BufAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctl.md)"><strong>BufAfterReqCompletedIntIoctl</strong></a>ルールは、要求が完了した後、そのバッファーにアクセスできないことを指定します ( <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>Evtiointernaldevicecontrol</em></a>コールバック関数内でのみ)。 バッファーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)"><strong>WdfRequestRetrieveOutputBuffer</strong></a> 、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)"><strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong></a> 、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)"><strong>WdfRequestRetrieveInputBuffer</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)"><strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong></a>を呼び出すことによって取得されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"><strong>BufAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedintioctla.md)"><strong>BufAfterReqCompletedIntIoctlA</strong></a>ルールは、要求が完了した後、そのバッファーにアクセスできないことを確認します ( <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>Evtiointernaldevicecontrol</em></a>コールバックのみ)。 バッファーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)"><strong>WdfRequestRetrieveInputBuffer</strong></a> 、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)"><strong>WdfRequestRetrieveOutputBuffer</strong></a> 、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserInputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)"><strong>WdfRequestRetrieveUnsafeUserInputBuffer</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer" data-raw-source="[&lt;strong&gt;WdfRequestRetrieveUnsafeUserOutputBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)"><strong>WdfRequestRetrieveUnsafeUserOutputBuffer</strong></a>を呼び出すことによって取得されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"><strong>BufAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-bufafterreqcompletedioctla.md)"><strong>BufAfterReqCompletedIoctlA</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>Evtiodevicecontrol</em></a>コールバック関数内で i/o 要求の完了後に取得される i/o 要求バッファーにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"><strong>BufAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-bufafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedRead&lt;/strong&gt;](kmdf-bufafterreqcompletedread.md)"><strong>BufAfterReqCompletedRead</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>コールバック関数内で、i/o 要求の完了後に取得された i/o 要求バッファーにアクセスできないことを指定します。 可能なバッファーアクセスメソッドとして機能する DDIs は14個あります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedReadA&lt;/strong&gt;](kmdf-bufafterreqcompletedreada.md)"><strong>BufAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedReadA ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>コールバック関数内で、i/o 要求の完了後に取得された i/o 要求バッファーにアクセスできないことを指定します。 可能なバッファーアクセスメソッドとして機能する DDIs は14個あります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWrite&lt;/strong&gt;](kmdf-bufafterreqcompletedwrite.md)"><strong>BufAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWrite ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>Evtiowrite</em></a>コールバック関数内で i/o 要求の完了後に取得される i/o 要求バッファーにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-bufafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;BufAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-bufafterreqcompletedwritea.md)"><strong>BufAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p>BufAfterReqCompletedWriteA ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>Evtiowrite</em></a>コールバック関数内で i/o 要求の完了後に取得される i/o 要求バッファーにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"><strong>ChildDeviceInitApi</strong></a></p></td>
<td align="left"><p><a href="kmdf-childdeviceinitapi.md" data-raw-source="[&lt;strong&gt;ChildDeviceInitApi&lt;/strong&gt;](kmdf-childdeviceinitapi.md)"><strong>Childdeviceinitapi</strong></a>規則では、子デバイスに対して、ドライバーが子デバイスオブジェクトの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>メソッドを呼び出す前に、フレームワークデバイスオブジェクトの初期化メソッドを呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldevicedeleted.md" data-raw-source="[&lt;strong&gt;ControlDeviceDeleted&lt;/strong&gt;](kmdf-controldevicedeleted.md)"><strong>ControlDeviceDeleted</strong></a></p></td>
<td align="left"><p>制御 Devicedeleted ルールは、PnP ドライバーがコントロールデバイスオブジェクトを作成する場合、ドライバーは、ドライバーがアンロードされる前に、いずれかのクリーンアップコールバック関数でコントロールデバイスオブジェクトを削除する必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-controldeviceinitapi.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAPI&lt;/strong&gt;](kmdf-controldeviceinitapi.md)"><strong>ControlDeviceInitAPI</strong></a></p></td>
<td align="left"><p>ControlDeviceInitAPI ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>Wdfcontroldeviceinitallocate</strong></a>と、コントロールデバイスの<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"><strong>WDFDEVICE_INIT</strong></a>構造を設定するその他すべてのデバイスオブジェクト初期化 DDIs を、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>の前に呼び出す必要があることを指定します。コントロールデバイス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"><strong>CtlDeviceFinishInitDeviceAdd</strong></a></p></td>
<td align="left"><p><a href="kmdf-ctldevicefinishinitdeviceadd.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDeviceAdd&lt;/strong&gt;](kmdf-ctldevicefinishinitdeviceadd.md)"><strong>CtlDeviceFinishInitDeviceAdd</strong></a>ルールでは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><em>Evtdriverdeviceadd</em></a>コールバック関数にコントロールデバイスオブジェクトを作成する場合、デバイスが作成されてから、その前にを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)"><strong>初期化</strong></a>する必要があることを指定します。これは、 <strong>Evtdriverdeviceadd</strong>コールバック関数から終了します。 このルールは、PnP 以外のドライバーには適用されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-ctldevicefinishinitdrentry.md" data-raw-source="[&lt;strong&gt;CtlDeviceFinishInitDrEntry&lt;/strong&gt;](kmdf-ctldevicefinishinitdrentry.md)"><strong>CtlDeviceFinishInitDrEntry</strong></a></p></td>
<td align="left"><p>CtlDeviceFinishInitDrEntry ルールでは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)"><strong>Driverentry</strong></a>コールバック関数にコントロールデバイスオブジェクトを作成する場合、デバイスが作成されてから終了する前に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing" data-raw-source="[&lt;strong&gt;WdfControlFinishInitializing&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)"></a> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[&lt;em&gt;EvtDriverDeviceAdd&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><em>wdfcontrolfinish を呼び出す必要があることを指定します。EvtDriverDeviceAdd</em></a>コールバック関数。 このルールは、PnP 以外のドライバーには適用されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"><strong>DeviceCreateFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-devicecreatefail.md" data-raw-source="[&lt;strong&gt;DeviceCreateFail&lt;/strong&gt;](kmdf-devicecreatefail.md)"><strong>DeviceCreateFail</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>の呼び出しが失敗したときに EVT_WDF_DRIVER_DEVICE_ADD がエラー状態を返すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"><strong>DeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-deviceinitallocate.md" data-raw-source="[&lt;strong&gt;DeviceInitAllocate&lt;/strong&gt;](kmdf-deviceinitallocate.md)"><strong>Deviceinitallocate</strong></a>ルールでは、PDO デバイスまたはコントロールデバイスオブジェクトに対して、フレームワークのデバイスオブジェクト初期化メソッド<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"><strong>wdfpdoinitallocate</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>wdfcontroldeviceinitallocate</strong></a>をドライバーの前に呼び出す必要があることを指定します。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-deviceinitapi.md" data-raw-source="[&lt;strong&gt;DeviceInitAPI&lt;/strong&gt;](kmdf-deviceinitapi.md)"><strong>DeviceInitAPI</strong></a></p></td>
<td align="left"><p>FDO デバイスの場合、ドライバーがデバイスオブジェクトの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>メソッドを呼び出す前に、フレームワークのデバイスオブジェクト初期化メソッドとフレームワーク FDO 初期化メソッドを呼び出す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"><strong>DoubleDeviceInitFree</strong></a></p></td>
<td align="left"><p><a href="kmdf-doubledeviceinitfree.md" data-raw-source="[&lt;strong&gt;DoubleDeviceInitFree&lt;/strong&gt;](kmdf-doubledeviceinitfree.md)"><strong>DoubleDeviceInitFree</strong></a>規則は、ドライバーがデバイス初期化構造を2回解放しないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"><strong>DriverCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-drivercreate.md" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](kmdf-drivercreate.md)"><strong>Drivercreate</strong></a>ルールは、カーネルモードドライバーフレームワーク (kmdf) を使用するドライバーが、 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)"><strong>drivercreate</strong></a>ルーチン内からフレームワークドライバーオブジェクトを作成するために、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate" data-raw-source="[&lt;strong&gt;WdfDriverCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)"><strong>wdfdrivercreate</strong></a>メソッドを呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecallback.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCallback&lt;/strong&gt;](kmdf-initfreedevicecallback.md)"><strong>InitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCallback 規則は、ドライバーが新しいフレームワークデバイスオブジェクトの初期化中にエラーを検出した場合、およびドライバーがの呼び出しから<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"><strong>WDFDEVICE_INIT</strong></a>構造体を受け取った場合に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>Wdfdeviceinitfree</strong></a>を呼び出す必要があることを指定します。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>Wdfcontroldeviceinitallocate</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"><strong>InitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreate.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreate&lt;/strong&gt;](kmdf-initfreedevicecreate.md)"><strong>InitFreeDeviceCreate</strong></a>規則は、デバイスオブジェクトの初期化メソッドの1つでエラーが発生した場合、およびドライバーが WDFDEVICE_INIT を受け取った場合に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>ではなく<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>wdfdeviceinitfree</strong></a>を呼び出す必要があることを指定します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"></a> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>Wdfcontroldeviceinitallocate</strong></a>の呼び出しからの構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-initfreedevicecreatetype2.md)"><strong>InitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>InitFreeDeviceCreateType2 規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>Wdfdeviceinitfree</strong></a>を呼び出した後、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>を呼び出すことができないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"><strong>InitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;InitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-initfreedevicecreatetype4.md)"><strong>InitFreeDeviceCreateType4</strong></a>規則は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>を呼び出している間にエラーが発生し、ドライバーが呼び出しから<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"><strong>WDFDEVICE_INIT</strong></a>構造体を受け取った場合に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>wdfdeviceinitfree</strong></a>を呼び出す必要があることを指定します。を<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>Wdfcontroldeviceinitallocate に割り当て</strong></a>ます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"><strong>InitFreeNull</strong></a></p></td>
<td align="left"><p><a href="kmdf-initfreenull.md" data-raw-source="[&lt;strong&gt;InitFreeNull&lt;/strong&gt;](kmdf-initfreenull.md)"><strong>InitFreeNull</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[WDFDEVICE_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)">WDFDEVICE_INIT</a>構造体への<strong>NULL</strong>ポインターを使用して、DDIs をパラメーターとして受け取ることができないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctl.md)"><strong>MdlAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p>MdlAfterReqCompletedIntIoctl ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>Evtiointernaldevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にメモリ記述子リスト (MDL) にアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"><strong>MdlAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedintioctla.md)"><strong>MdlAfterReqCompletedIntIoctlA</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>Evtiointernaldevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にメモリ記述子リスト (MDL) にアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"><strong>MdlAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctl.md)"><strong>MdlAfterReqCompletedIoctl</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>Evtiodevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にメモリ記述子リスト (MDL) にアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"><strong>MdlAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-mdlafterreqcompletedioctla.md)"><strong>MdlAfterReqCompletedIoctlA</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>Evtiodevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にメモリ記述子リスト (MDL) にアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"><strong>MdlAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedRead&lt;/strong&gt;](kmdf-mdlafterreqcompletedread.md)"><strong>MdlAfterReqCompletedRead</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a> callback 関数内で、i/o 要求の完了後に取得されたメモリ記述子リスト (MDL) オブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"><strong>MdlAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedReadA&lt;/strong&gt;](kmdf-mdlafterreqcompletedreada.md)"><strong>MdlAfterReqCompletedReadA</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a> callback 関数内で、i/o 要求の完了後に取得されたメモリ記述子リスト (MDL) オブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"><strong>MdlAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWrite&lt;/strong&gt;](kmdf-mdlafterreqcompletedwrite.md)"><strong>MdlAfterReqCompletedWrite</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>Evtiowrite</em></a>コールバック関数内で、i/o 要求の完了後に取得されたメモリ記述子リスト (MDL) オブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"><strong>MdlAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-mdlafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MdlAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-mdlafterreqcompletedwritea.md)"><strong>MdlAfterReqCompletedWriteA</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>Evtiowrite</em></a>コールバック関数内で、i/o 要求の完了後に取得されたメモリ記述子リスト (MDL) オブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"><strong>MemAfterReqCompletedIntIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedintioctl.md)"><strong>MemAfterReqCompletedIntIoctl</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>Evtiointernaldevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedintioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedintioctla.md)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>Evtiointernaldevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"><strong>MemAfterReqCompletedIoctl</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctl.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctl&lt;/strong&gt;](kmdf-memafterreqcompletedioctl.md)"><strong>MemAfterReqCompletedIoctl</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>Evtiodevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedioctla.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](kmdf-memafterreqcompletedioctla.md)"><strong>MemAfterReqCompletedIoctlA</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>Evtiodevicecontrol</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"><strong>MemAfterReqCompletedRead</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedread.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedRead&lt;/strong&gt;](kmdf-memafterreqcompletedread.md)"><strong>MemAfterReqCompletedRead</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedreada.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](kmdf-memafterreqcompletedreada.md)"><strong>MemAfterReqCompletedReadA</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"><strong>MemAfterReqCompletedWrite</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwrite.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWrite&lt;/strong&gt;](kmdf-memafterreqcompletedwrite.md)"><strong>MemAfterReqCompletedWrite</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>Evtiowrite</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a></p></td>
<td align="left"><p><a href="kmdf-memafterreqcompletedwritea.md" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](kmdf-memafterreqcompletedwritea.md)"><strong>MemAfterReqCompletedWriteA</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>Evtiowrite</em></a>コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullcheck.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheck.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 規則は、ドライバーコード内の NULL 値がドライバーの後で逆参照されないことを検証します。 このルールは、次のいずれかの条件が満たされた場合に、欠陥を報告します。</p>
<ul>
<li>後で逆参照される NULL の割り当てがあります。</li>
<li>ドライバー内のプロシージャには、後で逆参照される可能性のあるグローバル/パラメーターがあります。また、ドライバーに明示的なチェックがあり、ポインターの初期値が NULL である可能性があることが示されています。</li>
</ul>
<p>NullCheck 規則違反では、最も関連性の高いコードステートメントが [トレースツリー] ウィンドウで強調表示されます。 レポート出力の操作の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)">静的ドライバーの検証ツールレポート</a>」と「<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer)">トレースビューアーに</a>ついて」を参照してください。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"><strong>PdoDeviceInitAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdodeviceinitapi.md" data-raw-source="[&lt;strong&gt;PdoDeviceInitAPI&lt;/strong&gt;](kmdf-pdodeviceinitapi.md)"><strong>PdoDeviceInitAPI</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"><strong>Wdfpdoinitallocate</strong></a>と、物理デバイスオブジェクト (PDO) の<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init" data-raw-source="[&lt;strong&gt;WDFDEVICE_INIT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)"><strong>WDFDEVICE_INIT</strong></a>構造を設定するその他すべてのデバイスオブジェクト初期化 DDIs を、ドライバーが呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>前に呼び出す必要があることを指定します。</strong></a>PDO の WdfDeviceCreate。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"><strong>PdoInitFreeDeviceCallback</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecallback.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCallback&lt;/strong&gt;](kmdf-pdoinitfreedevicecallback.md)"><strong>PdoInitFreeDeviceCallback</strong></a>規則は、ドライバーが任意のフレームワークデバイスオブジェクト初期化関数を呼び出すときにエラーが発生した場合に、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>Wdfdeviceinitfree</strong></a>を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"><strong>PdoInitFreeDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreate.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreate&lt;/strong&gt;](kmdf-pdoinitfreedevicecreate.md)"><strong>PdoInitFreeDeviceCreate</strong></a>規則は、デバイスオブジェクトの初期化関数の1つでエラーが発生した場合、およびドライバーが WDFDEVICE_INIT を受け取った場合に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>ではなく<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>wdfdeviceinitfree</strong></a>を呼び出す必要があることを指定します。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"><strong>Wdfpdoinitallocate</strong></a>の呼び出しからの構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype2.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType2&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype2.md)"><strong>PdoInitFreeDeviceCreateType2</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType2 規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>Wdfdeviceinitfree</strong></a>を呼び出した後、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>を呼び出すことができないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-pdoinitfreedevicecreatetype4.md" data-raw-source="[&lt;strong&gt;PdoInitFreeDeviceCreateType4&lt;/strong&gt;](kmdf-pdoinitfreedevicecreatetype4.md)"><strong>PdoInitFreeDeviceCreateType4</strong></a></p></td>
<td align="left"><p>PdoInitFreeDeviceCreateType4 規則は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>を呼び出したときにエラーが発生した場合に、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree" data-raw-source="[&lt;strong&gt;WdfDeviceInitFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)"><strong>Wdfdeviceinitfree</strong></a>を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"><strong>ControlDeviceInitAllocate</strong></a></p></td>
<td align="left"><p><a href="kmdf-controldeviceinitallocate.md" data-raw-source="[&lt;strong&gt;ControlDeviceInitAllocate&lt;/strong&gt;](kmdf-controldeviceinitallocate.md)"><strong>Controldeviceinitallocate</strong></a>ルールは、コントロールデバイスオブジェクトに対して、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>を呼び出す前に、フレームワークデバイスオブジェクト初期化メソッド<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate" data-raw-source="[&lt;strong&gt;WdfControlDeviceInitAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)"><strong>Wdfcontroldeviceinitallocate</strong></a>を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"><strong>InputBufferAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-inputbufferapi.md" data-raw-source="[&lt;strong&gt;InputBufferAPI&lt;/strong&gt;](kmdf-inputbufferapi.md)"><strong>Inputbufferapi</strong></a>ルールでは、バッファー取得のための正しい DDIs が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>callback 関数で使用されることを指定します。 <em>EvtIoRead</em> callback 関数内では、バッファーを取得するために次の DDIs を呼び出すことはできません。</p></td>
</tr>
</tbody>
</table>

 

**DDI 使用規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[規則セット]** で **[ddiusage]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**ddiusage. sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 






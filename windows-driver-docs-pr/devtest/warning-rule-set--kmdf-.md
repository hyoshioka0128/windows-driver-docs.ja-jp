---
title: 警告ルールセット (KMDF)
description: これらのルールを使用して、ドライバーがさまざまなコンテキストで Irp を正しく処理できること、および Microsoft の推奨されるベストプラクティスに従うことを確認します。
ms.assetid: 0C012253-9FBD-4B5C-9A93-AF72405EF3E4
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3c050f97dfaec691cc7ab71dc13c5e5eb86877a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839255"
---
# <a name="warning-rule-set-kmdf"></a>警告ルールセット (KMDF)


これらのルールを使用して、ドライバーがさまざまなコンテキストで Irp を正しく処理できること、および Microsoft の推奨されるベストプラクティスに従うことを確認します。

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
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"><strong>DeferredRequestCompleted</strong></a></p></td>
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"><strong>DeferredRequestCompleted</strong></a>ルールは、ドライバーの既定の i/o キューに提示された i/o 要求がコールバック関数では完了せず、後で処理するために遅延される場合、遅延処理のコールバックで要求を完了する必要があることを指定します。関数。要求が転送されてフレームワークに配信される場合、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"><strong>Wdfrequeststopacknowledge</strong></a>メソッドが呼び出されない場合はです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-driverattributechanged.md" data-raw-source="[&lt;strong&gt;DriverAttributeChanged&lt;/strong&gt;](kmdf-driverattributechanged.md)"><strong>Driver属性の Echanged</strong></a></p></td>
<td align="left"><p><a href="kmdf-driverattributechanged.md" data-raw-source="[&lt;strong&gt;DriverAttributeChanged&lt;/strong&gt;](kmdf-driverattributechanged.md)"><strong>Driverの echanged</strong></a>ルールでは、ドライバーが kmdf ドライバーの実行レベルまたは同期スコープを変更してはならないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-drvackiostop.md" data-raw-source="[&lt;strong&gt;DrvAckIoStop&lt;/strong&gt;](kmdf-drvackiostop.md)"><strong>DrvAckIoStop</strong></a></p></td>
<td align="left"><p><a href="kmdf-drvackiostop.md" data-raw-source="[&lt;strong&gt;DrvAckIoStop&lt;/strong&gt;](kmdf-drvackiostop.md)"><strong>DrvAckIoStop</strong></a>ルールは、ドライバーが保留中の要求を認識しているときに、その電源管理キューの電源が入っていないことを確認します。ドライバーは、それに応じて保留中の要求を確認、完了、またはキャンセルします。 自己管理型の i/o 要求の場合、ドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"><em>Evtdeviceselfmanagediosuspend</em></a>関数からこれらの要求を正しく処理する必要があります。 電源を切るときにこれらの要求を処理できないドライバーは、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure" data-raw-source="[&lt;strong&gt;Bug Check 0x9F: DRIVER_POWER_STATE_FAILURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)"><strong>バグチェック 0x9f: DRIVER_POWER_STATE_FAILURE</strong></a>を発生させます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtioresumegetparam.md" data-raw-source="[&lt;strong&gt;EvtIoResumeGetParam&lt;/strong&gt;](kmdf-evtioresumegetparam.md)"><strong>EvtIoResumeGetParam</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtioresumegetparam.md" data-raw-source="[&lt;strong&gt;EvtIoResumeGetParam&lt;/strong&gt;](kmdf-evtioresumegetparam.md)"><strong>Evtioresumegetparam</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters" data-raw-source="[&lt;strong&gt;WdfRequestGetParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)"><strong>Wdfrequestgetparameters</strong></a>が<strong>evtioresumegetparam</strong>コールバック関数内で呼び出されないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtiostopgetparam.md" data-raw-source="[&lt;strong&gt;EvtIoStopGetParam&lt;/strong&gt;](kmdf-evtiostopgetparam.md)"><strong>EvtIoStopGetParam</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopgetparam.md" data-raw-source="[&lt;strong&gt;EvtIoStopGetParam&lt;/strong&gt;](kmdf-evtiostopgetparam.md)"><strong>Evtiostopgetparam</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters" data-raw-source="[&lt;strong&gt;WdfRequestGetParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)"><strong>Wdfrequestgetparameters</strong></a>が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>evtiostop</em></a>コールバック内で呼び出されないことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtiostopresume.md" data-raw-source="[&lt;strong&gt;EvtIoStopResume&lt;/strong&gt;](kmdf-evtiostopresume.md)"><strong>EvtIoStopResume</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopresume.md" data-raw-source="[&lt;strong&gt;EvtIoStopResume&lt;/strong&gt;](kmdf-evtiostopresume.md)"><strong>Evtiostopresume</strong></a>ルールでは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>Evtiostop</em></a>コールバック関数を登録し、<em>キューへ</em>パラメーターが FALSE に等しい<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"><strong>wdfrequeststopacknowledge</strong></a>を呼び出すと、ドライバーはを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>登録する必要があることを指定します。EvtIoResume</em></a> callback 関数。 フレームワークは、デバイスが D0 状態に再び入ると、 <strong>EvtIoResume</strong> callback 関数に要求を配信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtsurpriseremovenorequestcomplete.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoRequestComplete&lt;/strong&gt;](kmdf-evtsurpriseremovenorequestcomplete.md)"><strong>EvtSurpriseRemoveNoRequestComplete</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtsurpriseremovenorequestcomplete.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoRequestComplete&lt;/strong&gt;](kmdf-evtsurpriseremovenorequestcomplete.md)"><strong>EvtSurpriseRemoveNoRequestComplete</strong></a>規則は、WDF ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a>コールバックからの要求を完了できないように指定します。代わりに、自己管理型の i/o コールバック関数を使用する必要があります。 <em>EvtDeviceSurpriseRemoval</em>コールバックが電源ダウンパスと同期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-fdopowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;FDOPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-fdopowerpolicyownerapi.md)"><strong>FDOPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-fdopowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;FDOPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-fdopowerpolicyownerapi.md)"><strong>Fdopowerpolicyownerapi</strong></a>ルールでは、FDO ドライバーが電源ポリシーの所有権を放棄する場合、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetPowerPolicyEventCallbacks&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)"><strong>Wdfdeviceinitsetpowerpolicyeventcallbacks バック</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignSxWakeSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)"><strong>の各メソッドを指定します。WdfDeviceAssignSxWakeSettings</strong></a>は、ドライバーが電源ポリシーの所有者である実行パスでのみ呼び出すことができます。 SDV は、このルールに対して警告を発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-nocancelfromevtsurpriseremove.md" data-raw-source="[&lt;strong&gt;NoCancelFromEvtSurpriseRemove&lt;/strong&gt;](kmdf-nocancelfromevtsurpriseremove.md)"><strong>NoCancelFromEvtSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="kmdf-nocancelfromevtsurpriseremove.md" data-raw-source="[&lt;strong&gt;NoCancelFromEvtSurpriseRemove&lt;/strong&gt;](kmdf-nocancelfromevtsurpriseremove.md)"><strong>NoCancelFromEvtSurpriseRemove</strong></a>規則は、WDF ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a>コールバック関数からの要求をキャンセルしないように指定します。代わりに、自己管理型の i/o コールバック関数を使用する必要があります。 <em>EvtDeviceSurpriseRemoval</em> callback 関数が、電源を切るパスと同期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pagedcodeatd0.md" data-raw-source="[&lt;strong&gt;PagedCodeAtD0&lt;/strong&gt;](kmdf-pagedcodeatd0.md)"><strong>PagedCodeAtD0</strong></a></p></td>
<td align="left"><p><a href="kmdf-pagedcodeatd0.md" data-raw-source="[&lt;strong&gt;PagedCodeAtD0&lt;/strong&gt;](kmdf-pagedcodeatd0.md)"><strong>PagedCodeAtD0</strong></a>ルールでは、電源コードパス内のコールバック関数内で、ドライバーがコードをページング可能としてマークしてはいけないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-parentobjectcheck.md" data-raw-source="[&lt;strong&gt;ParentObjectCheck&lt;/strong&gt;](kmdf-parentobjectcheck.md)"><strong>ParentObjectCheck</strong></a></p></td>
<td align="left"><p><a href="kmdf-parentobjectcheck.md" data-raw-source="[&lt;strong&gt;ParentObjectCheck&lt;/strong&gt;](kmdf-parentobjectcheck.md)"><strong>ParentObjectCheck</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes" data-raw-source="[&lt;strong&gt;WDF_OBJECT_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)"><strong>WDF_OBJECT_ATTRIBUTES</strong></a>構造体を使用して親オブジェクトを指定して、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate" data-raw-source="[&lt;strong&gt;WdfMemoryCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)"><strong>wdfmemorycreate</strong></a>を呼び出す必要があることを指定します。 ドライバーがフレームワークのメモリオブジェクトの親オブジェクトを設定していない場合、フレームワークはドライバーを既定の親として設定します。これにより、ドライバーオブジェクトがアンロードされるまで、ドライバーがフレームワークメモリオブジェクトを明示的に削除しない限り、ドライバーはメモリに残ります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqnotcanceledlocal.md" data-raw-source="[&lt;strong&gt;ReqNotCanceledLocal&lt;/strong&gt;](kmdf-reqnotcanceledlocal.md)"><strong>ReqNotCanceledLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqnotcanceledlocal.md" data-raw-source="[&lt;strong&gt;ReqNotCanceledLocal&lt;/strong&gt;](kmdf-reqnotcanceledlocal.md)"><strong>ReqNotCanceledLocal</strong></a>ルールでは、キャンセル可能とマークされた要求が既定の i/o キューコールバック関数で完了した場合に、完了前に i/o 要求で<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestUnmarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)"><strong>Wdfrequestunmarkcancelable</strong></a>メソッドを呼び出す必要があることを指定します。 要求が取り消された場合は、 <strong>Wdfrequestunmarkcancelable</strong>を呼び出す前に、i/o 要求を完了する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqsendfail.md" data-raw-source="[&lt;strong&gt;ReqSendFail&lt;/strong&gt;](kmdf-reqsendfail.md)"><strong>ReqSendFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqsendfail.md" data-raw-source="[&lt;strong&gt;ReqSendFail&lt;/strong&gt;](kmdf-reqsendfail.md)"><strong>ReqSendFail</strong></a>規則は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>Wdfrequestsend</strong></a>メソッドが失敗する可能性がある場合に、ドライバーで正しい完了状態を設定する必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestcompletedlocal.md" data-raw-source="[&lt;strong&gt;RequestCompletedLocal&lt;/strong&gt;](kmdf-requestcompletedlocal.md)"><strong>RequestCompletedLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestcompletedlocal.md" data-raw-source="[&lt;strong&gt;RequestCompletedLocal&lt;/strong&gt;](kmdf-requestcompletedlocal.md)"><strong>RequestCompletedLocal</strong></a>ルールでは、いずれかの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"><em>Evtiodefault</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"><em>EvtIoRead</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>evtiodefault</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"><em>Evtiodevicecontrol</em></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"><em>evtiointernaldevicecontrol</em></a>コールバックで i/o 要求が完了しない場合に指定します。関数、およびコールバック関数内の要求で<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"><strong>Wdfrequestmarkcancelable</strong></a>が呼び出されなかった場合、ドライバーのコードで要求の完了に問題がある可能性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestforurbxrb.md" data-raw-source="[&lt;strong&gt;RequestForUrbXrb&lt;/strong&gt;](kmdf-requestforurbxrb.md)"><strong>RequestForUrbXrb</strong></a></p></td>
<td align="left"><p>クライアントドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a>を呼び出し、WDF_USB_DEVICE_CREATE_CONFIG 構造体でクライアントコントラクトバージョン USBD_CLIENT_CONTRACT_VERSION_602 を指定している場合 (用の USB ドライバースタックの新機能を使用する場合)。Windows 8) DDIs を内部的に使用する場合、次のいずれかの事前条件が適用される場合にのみ、 <em>urb コンテキスト</em>が使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-syncreqsend.md" data-raw-source="[&lt;strong&gt;SyncReqSend&lt;/strong&gt;](kmdf-syncreqsend.md)"><strong>SyncReqSend</strong></a></p></td>
<td align="left"><p><a href="kmdf-syncreqsend.md" data-raw-source="[&lt;strong&gt;SyncReqSend&lt;/strong&gt;](kmdf-syncreqsend.md)"><strong>Syncreqsend</strong></a>ルールでは、同期固有の kmdf デバイスドライバーのインターフェイスメソッドを使用してすべての同期送信要求を実行し、メソッドに0以外のタイムアウト値が設定されていることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-syncreqsend2.md" data-raw-source="[&lt;strong&gt;SyncReqSend2&lt;/strong&gt;](kmdf-syncreqsend2.md)"><strong>SyncReqSend2</strong></a></p></td>
<td align="left"><p><a href="kmdf-syncreqsend2.md" data-raw-source="[&lt;strong&gt;SyncReqSend2&lt;/strong&gt;](kmdf-syncreqsend2.md)"><strong>SyncReqSend2</strong></a>ルールは、同期要求の送信に0以外のタイムアウト値が設定されていることを指定します。</p></td>
</tr>
</tbody>
</table>

 

**警告ルールセットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[警告]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**Warning. sdv**を指定します。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 






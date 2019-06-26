---
title: 警告の規則セット (KMDF)
description: これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。
ms.assetid: 0C012253-9FBD-4B5C-9A93-AF72405EF3E4
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 65df2dd5ba71b62478a625e827330711207a463e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363748"
---
# <a name="warning-rule-set-kmdf"></a>警告の規則セット (KMDF)


これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。

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
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"> <strong>DeferredRequestCompleted</strong> </a>ルールことを指定する場合に、I/O 要求が表示されるドライバーの既定の I/O キュー コールバック関数では、完了していない、後で処理の遅延が、遅延処理のコールバック関数での要求の完了する必要がありますか、要求が転送され、フレームワークに配信される場合を除き、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"> <strong>WdfRequestStopAcknowledge</strong> </a>メソッドと呼ばれる。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-driverattributechanged.md" data-raw-source="[&lt;strong&gt;DriverAttributeChanged&lt;/strong&gt;](kmdf-driverattributechanged.md)"><strong>DriverAttributeChanged</strong></a></p></td>
<td align="left"><p><a href="kmdf-driverattributechanged.md" data-raw-source="[&lt;strong&gt;DriverAttributeChanged&lt;/strong&gt;](kmdf-driverattributechanged.md)"> <strong>DriverAttributeChanged</strong> </a>ルールでは、ドライバーは、KMDF ドライバーの実行レベルまたは同期スコープを変更できないことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-drvackiostop.md" data-raw-source="[&lt;strong&gt;DrvAckIoStop&lt;/strong&gt;](kmdf-drvackiostop.md)"><strong>DrvAckIoStop</strong></a></p></td>
<td align="left"><p><a href="kmdf-drvackiostop.md" data-raw-source="[&lt;strong&gt;DrvAckIoStop&lt;/strong&gt;](kmdf-drvackiostop.md)"> <strong>DrvAckIoStop</strong> </a>ルールは、電源管理対象のキューが電源の切断を取得して、ドライバーの確認が完了したら、またはキャンセル中に、ドライバーは保留中の要求を認識を検証、保留中それに応じて要求します。 自己管理型の I/O 要求の場合、ドライバーも正しくこれらによる要求の処理からその<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)"> <em>EvtDeviceSelfManagedIoSuspend</em> </a>関数。 電源オフ時にこれらの要求を処理するために失敗したドライバーが引き起こす<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure" data-raw-source="[&lt;strong&gt;Bug Check 0x9F: DRIVER_POWER_STATE_FAILURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure)"> <strong>0x9F のバグ チェック。DRIVER_POWER_STATE_FAILURE</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtioresumegetparam.md" data-raw-source="[&lt;strong&gt;EvtIoResumeGetParam&lt;/strong&gt;](kmdf-evtioresumegetparam.md)"><strong>EvtIoResumeGetParam</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtioresumegetparam.md" data-raw-source="[&lt;strong&gt;EvtIoResumeGetParam&lt;/strong&gt;](kmdf-evtioresumegetparam.md)"> <strong>EvtIoResumeGetParam</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters" data-raw-source="[&lt;strong&gt;WdfRequestGetParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)"> <strong>WdfRequestGetParameters</strong> </a>内では呼び出されません、 <strong>EvtIoResumeGetParam</strong>コールバック関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtiostopgetparam.md" data-raw-source="[&lt;strong&gt;EvtIoStopGetParam&lt;/strong&gt;](kmdf-evtiostopgetparam.md)"><strong>EvtIoStopGetParam</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopgetparam.md" data-raw-source="[&lt;strong&gt;EvtIoStopGetParam&lt;/strong&gt;](kmdf-evtiostopgetparam.md)"> <strong>EvtIoStopGetParam</strong> </a>ことを確認しますルール<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters" data-raw-source="[&lt;strong&gt;WdfRequestGetParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)"> <strong>WdfRequestGetParameters</strong> </a>内では呼び出されません<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>コールバック。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtiostopresume.md" data-raw-source="[&lt;strong&gt;EvtIoStopResume&lt;/strong&gt;](kmdf-evtiostopresume.md)"><strong>EvtIoStopResume</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopresume.md" data-raw-source="[&lt;strong&gt;EvtIoStopResume&lt;/strong&gt;](kmdf-evtiostopresume.md)"> <strong>EvtIoStopResume</strong> </a>ルール指定する場合は、ドライバーは、登録、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>コールバック関数に呼び出し<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"> <strong>WdfRequestStopAcknowledge</strong> </a>で、<em>をもう一度キュー</em>パラメーターと等しい<strong>FALSE</strong>、ドライバーを登録する必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em> </a>コールバック関数。 フレームワークへの要求を提供する、 <strong>EvtIoResume</strong>デバイス D0 状態をもう一度入力するときのコールバック関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtsurpriseremovenorequestcomplete.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoRequestComplete&lt;/strong&gt;](kmdf-evtsurpriseremovenorequestcomplete.md)"><strong>EvtSurpriseRemoveNoRequestComplete</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtsurpriseremovenorequestcomplete.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoRequestComplete&lt;/strong&gt;](kmdf-evtsurpriseremovenorequestcomplete.md)"> <strong>EvtSurpriseRemoveNoRequestComplete</strong> </a>ルールでは、WDF ドライバーからの要求を完了べきではないことを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"> <em>EvtDeviceSurpriseRemoval</em></a>コールバック、代わりに自己管理される I/O のコールバック関数を使用する必要があります。 <em>EvtDeviceSurpriseRemoval</em>コールバックは、電源のパスと同期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-fdopowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;FDOPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-fdopowerpolicyownerapi.md)"><strong>FDOPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-fdopowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;FDOPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-fdopowerpolicyownerapi.md)"> <strong>FDOPowerPolicyOwnerAPI</strong> </a>規則で指定された場合、メソッド、電源ポリシー所有権を解放する、FDO ドライバー <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetPowerPolicyEventCallbacks&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)"> <strong>WdfDeviceInitSetPowerPolicyEventCallbacks</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"> <strong>WdfDeviceAssignS0IdleSettings</strong></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignSxWakeSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)"> <strong>WdfDeviceAssignSxWakeSettings</strong> </a>のみ呼び出せる実行パスでドライバーの場所が電源ポリシーの所有者。 SDV は、この規則の警告を発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-nocancelfromevtsurpriseremove.md" data-raw-source="[&lt;strong&gt;NoCancelFromEvtSurpriseRemove&lt;/strong&gt;](kmdf-nocancelfromevtsurpriseremove.md)"><strong>NoCancelFromEvtSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="kmdf-nocancelfromevtsurpriseremove.md" data-raw-source="[&lt;strong&gt;NoCancelFromEvtSurpriseRemove&lt;/strong&gt;](kmdf-nocancelfromevtsurpriseremove.md)"> <strong>NoCancelFromEvtSurpriseRemove</strong> </a>ルールでは、WDF のドライバーがからの要求を取り消すことはできませんを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"> <em>EvtDeviceSurpriseRemoval</em> </a>コールバック関数では、代わりに自己管理される I/O のコールバック関数を使用する必要があります。 <em>EvtDeviceSurpriseRemoval</em>コールバック関数は、電源のパスと同期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-pagedcodeatd0.md" data-raw-source="[&lt;strong&gt;PagedCodeAtD0&lt;/strong&gt;](kmdf-pagedcodeatd0.md)"><strong>PagedCodeAtD0</strong></a></p></td>
<td align="left"><p><a href="kmdf-pagedcodeatd0.md" data-raw-source="[&lt;strong&gt;PagedCodeAtD0&lt;/strong&gt;](kmdf-pagedcodeatd0.md)"> <strong>PagedCodeAtD0</strong> </a>ルールでは、ドライバーがパワーアップ コード パスに含まれるコールバック関数内でページング可能としてコードをマークする必要がありますを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-parentobjectcheck.md" data-raw-source="[&lt;strong&gt;ParentObjectCheck&lt;/strong&gt;](kmdf-parentobjectcheck.md)"><strong>ParentObjectCheck</strong></a></p></td>
<td align="left"><p><a href="kmdf-parentobjectcheck.md" data-raw-source="[&lt;strong&gt;ParentObjectCheck&lt;/strong&gt;](kmdf-parentobjectcheck.md)"> <strong>ParentObjectCheck</strong> </a>ルールでは、そのドライバーを呼び出す必要がありますを指定します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate" data-raw-source="[&lt;strong&gt;WdfMemoryCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate)"> <strong>WdfMemoryCreate</strong> </a> を使用して、親オブジェクトを指定します。<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes" data-raw-source="[&lt;strong&gt;WDF_OBJECT_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)"><strong>WDF_OBJECT_ATTRIBUTES</strong> </a>構造体。 ドライバーが設定されていない場合、フレームワーク、framework メモリ オブジェクトの親オブジェクトは、ドライバーは、framework メモリ オブジェクトを削除しない限り、明示的にありますに残ったままとメモリ ドライバー オブジェクトがアンロードされるまでように、既定の親としてドライバーを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqnotcanceledlocal.md" data-raw-source="[&lt;strong&gt;ReqNotCanceledLocal&lt;/strong&gt;](kmdf-reqnotcanceledlocal.md)"><strong>ReqNotCanceledLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqnotcanceledlocal.md" data-raw-source="[&lt;strong&gt;ReqNotCanceledLocal&lt;/strong&gt;](kmdf-reqnotcanceledlocal.md)"> <strong>ReqNotCanceledLocal</strong> </a>ルール完了を指定する要求がキャンセル可能としてマークされている場合は、既定 I/O キュー コールバック関数で、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestUnmarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)"> <strong>WdfRequestUnmarkCancelable</strong> </a>完了前に、I/O 要求のメソッドを呼び出す必要があります。 呼び出す前に、要求が取り消された場合を除き、I/O 要求を完了する必要があります<strong>WdfRequestUnmarkCancelable</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqsendfail.md" data-raw-source="[&lt;strong&gt;ReqSendFail&lt;/strong&gt;](kmdf-reqsendfail.md)"><strong>ReqSendFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqsendfail.md" data-raw-source="[&lt;strong&gt;ReqSendFail&lt;/strong&gt;](kmdf-reqsendfail.md)"> <strong>ReqSendFail</strong> </a>ルールでは、ドライバーがの場合に適切な完了状態を設定する必要がありますを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)"> <strong>WdfRequestSend</strong> </a>メソッドが失敗する可能性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestcompletedlocal.md" data-raw-source="[&lt;strong&gt;RequestCompletedLocal&lt;/strong&gt;](kmdf-requestcompletedlocal.md)"><strong>RequestCompletedLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestcompletedlocal.md" data-raw-source="[&lt;strong&gt;RequestCompletedLocal&lt;/strong&gt;](kmdf-requestcompletedlocal.md)"> <strong>RequestCompletedLocal</strong> </a>ルールを指定するのいずれかで、I/O 要求を完了していない場合、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)"> <em>EvtIoDefault</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)"> <em>EvtIoRead</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)"> <em>EvtIoDeviceControl</em> </a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)"> <em>EvtIoInternalDeviceControl</em> </a>コールバック関数と if <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"> <strong>WdfRequestMarkCancelable</strong> </a>呼び出されていない、コールバック関数内での要求である可能性があります、問題、ドライバーのコードで要求を完了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestforurbxrb.md" data-raw-source="[&lt;strong&gt;RequestForUrbXrb&lt;/strong&gt;](kmdf-requestforurbxrb.md)"><strong>RequestForUrbXrb</strong></a></p></td>
<td align="left"><p>クライアント ドライバーを呼び出す場合<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"> <strong>WdfUsbTargetDeviceCreateWithParameters</strong> </a> WDF_USB_DEVICE_CREATE_CONFIG 内にクライアント コントラクト バージョン USBD_CLIENT_CONTRACT_VERSION_602 を指定します構造体 (USB ドライバー スタックの新しい機能を使用して、Windows 8 用) を Ddi、URB を内部的に使用するどのように使い分ければのみ<em>URB コンテキスト</em>次の前提条件のいずれかに該当する場合。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-syncreqsend.md" data-raw-source="[&lt;strong&gt;SyncReqSend&lt;/strong&gt;](kmdf-syncreqsend.md)"><strong>SyncReqSend</strong></a></p></td>
<td align="left"><p><a href="kmdf-syncreqsend.md" data-raw-source="[&lt;strong&gt;SyncReqSend&lt;/strong&gt;](kmdf-syncreqsend.md)"> <strong>SyncReqSend</strong> </a>ルールは、同期固有 KMDF デバイス ドライバー インターフェイス メソッドを使用してすべての同期送信要求が行われることと、メソッドがある、0 以外の場合のタイムアウト値の設定を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-syncreqsend2.md" data-raw-source="[&lt;strong&gt;SyncReqSend2&lt;/strong&gt;](kmdf-syncreqsend2.md)"><strong>SyncReqSend2</strong></a></p></td>
<td align="left"><p><a href="kmdf-syncreqsend2.md" data-raw-source="[&lt;strong&gt;SyncReqSend2&lt;/strong&gt;](kmdf-syncreqsend2.md)"> <strong>SyncReqSend2</strong> </a>ルールでは、同期要求の送信が 0 以外のタイムアウト値が設定を持つことを指定します。</p></td>
</tr>
</tbody>
</table>

 

**警告ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**警告**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Warning.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 






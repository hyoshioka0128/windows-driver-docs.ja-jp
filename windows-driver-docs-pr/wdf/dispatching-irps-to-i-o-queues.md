---
title: I/O キューへの IRP のディスパッチ
description: I/O キューへの IRP のディスパッチ
ms.assetid: 71872114-2A38-47FE-9D18-EF8923273811
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53d42ba9784373a7a2e61010b8fc55604987fe83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845277"
---
# <a name="dispatching-irps-to-io-queues"></a>I/O キューへの IRP のディスパッチ


\[KMDF と UMDF\] に適用されます

フレームワークベースのドライバーでは、受信する IRP のターゲットキューを動的に指定できます。 IRP を特定のキューにディスパッチするには、ドライバーで[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)メソッドを呼び出す必要があります。

通常、ドライバーは、 [*EvtdevicewdmiWdfDeviceWdmDispatchIrpToIoQueue プリプロセス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)または[*Evtdevicewdmiのディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数のいずれかから、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)を呼び出します。 最適なパフォーマンスを得るために、ほとんどのドライバーには両方のコールバック関数が用意されていません。

UMDF ドライバーでは、 [*Evtdevicewdmirpq ディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数を提供できますが、使用できるのは kmdf ドライバーだけで[*evtdevicewdmiのプリプロセス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)を提供でき  ことに**注意**してください。

 

ドライバーによって既に[*Evtdevicewdmiの前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)が提供されている場合は、それを使用してキューを動的に選択できます。 それ以外の場合は、 [*EvtdevicewdmiWdfDeviceWdmDispatchIrpToIoQueue ディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)を提供し、そのコールバック関数内から呼び出します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)

また、次の点に注意する必要があります。

-   I/o キューに IRP をディスパッチする別の方法として、[既定のキューを作成](creating-i-o-queues.md)した後、キューのハンドラー内から[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)を呼び出します。 この手法は KMDF 1.0 以降で使用できますが、[進行状況の上位キュー](guaranteeing-forward-progress-of-i-o-operations.md)ではうまく機能せず、一般に低速です。 代わりに[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)を使用することを検討してください。

-   [**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)を呼び出して[*Evtdevicewdmi*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)のコールバック関数を登録する場合、ドライバーは*MajorFunction*パラメーターを次のいずれかに設定する必要があります。 IRP\_MJ\_デバイス\_CONTROL、IRP\_MJ\_内部\_デバイス\_コントロール、IRP\_MJ\_READ、irp\_MJ\_WRITE です。 この要件は[*Evtdevicewdmiの前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)には適用されませんが、指定されたキューに動的にディスパッチできるのはこれらの種類の irp だけです。

-   [*Evtdevicewdmiの前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)に移動する irp には、スタックの場所が追加されています。 [*Evtdevicewdmiのディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)にアクセスする irp (以前の*Evtdevicewdmiのプリプロセス*の呼び出しなし) は、実行されません。

-   [*Evtdevicewdmiの前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)では、ドライバー定義のコンテキスト情報を送信することはできませんが、 [*evtdevicewdmiのディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)はできません。

## <a name="dispatching-non-preprocessed-irps"></a>プリプロセス以外の Irp のディスパッチ


ドライバーの[*Evtdevicewdmirpq ディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数から irp をディスパッチするには、次の手順に従います。

1.  この[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数から、ドライバーは[**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)を呼び出して[*Evtdevicewdmidriverdispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数を登録します。

    ターゲットが親デバイスの i/o キューの場合、KMDF ドライバーは[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出す前に[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)を呼び出す必要があります。 KMDF ドライバーにも[*Evtdevicewdmiの前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数が用意されている場合、このフレームワークは IRP が到着すると最初にその関数を呼び出します。 コールバック関数は、要求の前に[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)を呼び出して、IRP をフレームワークに返します。

2.  フレームワークは、ドライバーの[*Evtdevicewdmirpq ディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数を呼び出します。
3.  [*EvtdevicewdmiWdfDeviceWdmDispatchIrpToIoQueue dispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)内から、ドライバーは、両方で[**はなく、いずれか**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)の[**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)を呼び出すことができます。 KMDF ドライバーには、これらのメソッドを呼び出さずに、IRP を完了するか、保留中としてマークするオプションが追加されています。
4.  KMDF ドライバーによって\_ディスパッチ\_IRP\_が\_IO\_キューに設定されている場合は\_を呼び出し\_INCALLERCTX\_CALLBACK フラグを呼び出し、対象の i/o キューの事前進行を保証していません。次に、フレームワークは、指定されている場合、ドライバーの[*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)を呼び出します。 要求をプリプロセスした後、コールバック関数は、 [**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出してキューをキューに置いておくか、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出して完了する必要があります。

## <a name="dispatching-preprocessed-irps"></a>プリプロセス済み Irp のディスパッチ


ドライバーの[*Evtdevicewdmiの前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数から特定の i/o キューに irp をディスパッチするには、次の手順に従います。

1.  このドライバーは、 [**Wdfdeviceinit割り当て Wdmirpq Preprocesscallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)を呼び出すことによって、 [*Evtdevicewdmirpq*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)のコールバック関数を登録します。
2.  ターゲットが親デバイスの i/o キューの場合、ドライバーは[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)を呼び出します。
3.  [*EvtdevicewdmiWdfDeviceWdmDispatchIrpToIoQueue の前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)で、 *FLAGS*を\_WDF に設定[**して呼び出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)、IRP\_を\_IO\_キュー\_プリプロセスされた\_irp に\_ディスパッチします。
4.  ドライバーによって\_ディスパッチ\_IRP\_が\_IO\_キューに設定されている場合は\_を呼び出し\_INCALLERCTX\_コールバックフラグを呼び出し、対象の i/o キューの事前進行を保証していません。次に、フレームワークは、指定されている場合、ドライバーの[*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)を呼び出します。 コールバック関数が要求のプリプロセスを完了したら、 [**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出してキューをキューに置いておくか、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出して完了する必要があります。

 

 






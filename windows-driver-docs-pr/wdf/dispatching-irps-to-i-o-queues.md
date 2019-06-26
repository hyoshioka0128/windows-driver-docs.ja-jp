---
title: I/O キューへの IRP のディスパッチ
description: I/O キューへの IRP のディスパッチ
ms.assetid: 71872114-2A38-47FE-9D18-EF8923273811
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 937928e9b469bc2da4977d50bced0deeddc9ef25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377405"
---
# <a name="dispatching-irps-to-io-queues"></a>I/O キューへの IRP のディスパッチ


\[KMDF および UMDF に適用されます。\]

フレームワーク ベースのドライバーでは、着信 IRP のターゲット キューを動的に指定することができます。 特定のキューに IRP をディスパッチするドライバーを呼び出す必要があります、 [ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)メソッド。

通常、ドライバーを呼び出す[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)いずれかからその[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)または[*EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数。 最適なパフォーマンスをほとんどのドライバーには、両方のコールバック関数が提供されません。

**注**  A UMDF ドライバーを指定できます、 [ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数が唯一の KMDF ドライバーが提供できる[ *EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)します。

 

場合は、ドライバーが既に用意されています[ *EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)、それを使用して、キューを動的に選択することができます。 そうでない場合は、提供[ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)を呼び出すと[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)からそのコールバック内関数。

さらに、次の注意する必要があります。

-   I/O のキューに IRP のディスパッチ用の別の方法として[既定のキューを作成する](creating-i-o-queues.md)しから、キューのハンドラー内で呼び出す[ **WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)します。 この手法は以降 KMDF 1.0 で使用できますが、適切では機能しません[進行中のキューに転送](guaranteeing-forward-progress-of-i-o-operations.md)は一般に遅くなります。 使用を検討して[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)代わりにします。

-   呼び出すときに[ **WdfDeviceConfigureWdmIrpDispatchCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)を登録する、 [ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数ドライバーを設定する必要があります、 *MajorFunction*次のいずれかのパラメーター。IRP\_MJ\_DEVICE\_CONTROL, IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL, IRP\_MJ\_READ, IRP\_MJ\_WRITE. この要件には適用されません[ *EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)のみ、これらの型の Irp は指定されたキューを動的にディスパッチします。

-   移動 Irp [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)追加のスタックの場所があります。 移動 Irp [ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) (の直前の呼び出しなし*EvtDeviceWdmIrpPreprocess*) はありません。

-   [*EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)促進はしないドライバーによって定義されたコンテキストの情報を送信する一方[ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)は。

## <a name="dispatching-non-preprocessed-irps"></a>前処理された非 Irp のディスパッチ


ドライバーから Irp をディスパッチする[ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数を次の手順を使用します。

1.  その[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数では、ドライバー呼び出し[ **WdfDeviceConfigureWdmIrpDispatchCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)に登録、 [ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数。

    KMDF ドライバーを呼び出す必要があります、ターゲットが、親デバイスの I/O キューの場合は、 [ **WdfPdoInitAllowForwardingRequestToParent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)を呼び出す前に[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate). KMDF ドライバーにも指定されている場合、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数、フレームワーク関数を呼び出すそのまず IRP が到着するとします。 コールバック関数は、要求を前処理し、後に呼び出して[ **WdfDeviceWdmDispatchPreprocessedIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp) IRP をフレームワークに戻ります。

2.  フレームワークは、ドライバーの[ *EvtDeviceWdmIrpDispatch* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)コールバック関数。
3.  内から[ *EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)、呼び出すことができます、ドライバー [ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)または[ **WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)、両方ではないです。 KMDF ドライバーでは、どちらも、これらのメソッドを呼び出すことと代わりに、IRP の完了または保留中のマークの追加のオプションがあります。
4.  KMDF ドライバーが、WDF を設定した場合\_フォワード\_IRP\_TO\_IO\_キュー\_INVOKE\_INCALLERCTX\_コールバック フラグが有効になっていないことが保証処理を進行し、フレームワーク ターゲット I/O キューの呼び出し、ドライバーの[ *EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)指定されている場合、します。 要求を前処理した後、コールバック関数する必要がありますか、再生待ちに呼び出して[ **WdfDeviceEnqueueRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出して完了または[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete).

## <a name="dispatching-preprocessed-irps"></a>前処理済みの Irp のディスパッチ


ドライバーから Irp をディスパッチする[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数を特定の I/O キューは、次の手順を使用します。

1.  ドライバーのレジスタを[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数を呼び出して[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback).
2.  ドライバー呼び出し[ **WdfPdoInitAllowForwardingRequestToParent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent)ターゲットが、親デバイスの I/O キューの場合。
3.  [ *EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)、呼び出す[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)で*フラグ*WDF に設定\_フォワード\_IRP\_TO\_IO\_キュー\_前処理された\_IRP します。
4.  ドライバーは WDF を設定した場合\_フォワード\_IRP\_TO\_IO\_キュー\_INVOKE\_INCALLERCTX\_コールバック フラグが有効になっていないと転送保証ターゲット I/O キューの場合、フレームワークの進行状況の呼び出し、ドライバーの[ *EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)指定されている場合、します。 コールバック関数は、要求の前処理が完了したら後に、する必要がありますか、再生待ちに呼び出して[ **WdfDeviceEnqueueRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出して完了または[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

 

 






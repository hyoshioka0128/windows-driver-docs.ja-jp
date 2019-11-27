---
title: IRP の前処理と後処理
description: IRP の前処理と後処理
ms.assetid: a0e14ae6-a06e-4c24-8b64-b56f485cf9ff
keywords:
- Irp の前処理の WDK KMDF
- 後処理の Irp WDK KMDF
- WDM Irp WDK KMDF、前処理および後処理
- Irp WDK KMDF、前処理および後処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90a32e3cb8abbc171e4cbb90f56457d650982d40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842235"
---
# <a name="preprocessing-and-postprocessing-irps"></a>IRP の前処理と後処理


\[は KMDF にのみ適用され\]

フレームワークが IRP を処理する前または後に、ドライバーが i/o 要求パケット (IRP) を受け取る必要がある場合、ドライバーは[**Wdfdeviceinit割り当て Wdmirpq Preprocesscallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)を呼び出して、に対して[*Evtdevicewdmiの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)イベントコールバック関数を登録できます。主要なコードに関連付けられている特定のマイナー i/o 関数コード (必要に応じて)。 その後、指定されたメジャーおよびマイナー関数コードを含む IRP がドライバーによって受信されると、フレームワークはドライバーの*Evtdevicewdmiのプリプロセス*コールバック関数を呼び出します。

[*Evtdevicewdmi、前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数は、irp をプリプロセスするために必要な処理を実行できます。その後、ドライバーが irp を処理している場合を除き、 [**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)を呼び出して、irp をフレームワークに返す必要があります。 [フレームワークでは、はサポートされていません](handling-an-irp-that-the-framework-does-not-support.md)。

ドライバーが[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)を呼び出した後、フレームワークは、ドライバーに[*Evtdevicewdmi 前処理*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数が提供されていない場合と同じ方法で IRP を処理します。 IRP の i/o 関数コードが、フレームワークがドライバーに渡すものである場合、ドライバーは要求オブジェクトとして IRP を再度受信します。

低いレベルのドライバーが irp を完了した後に、ドライバーが irp を後処理に渡す必要がある場合、ドライバーの[*evtdevicewdmiWdfDeviceWdmDispatchPreprocessedIrp*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数は[**iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定してから、このルーチンで[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)を呼び出すことができます。

ドライバーが[**Wdfdeviceinit割り当て Wdmirpq Preprocesscallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)を呼び出した後、このフレームワークにより、i/o マネージャーは、すべての irp に i/o[スタック位置](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations)を追加して、 [*evtdevicewdmirpq*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数がを設定できるようにします。[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチン。 コールバック関数は、 [**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)を呼び出す前に、IRP の i/o スタック位置ポインターを更新する必要があります。

### <a name="calling-wdfdevicewdmdispatchpreprocessedirp"></a>WdfDeviceWdmDispatchPreprocessedIrp の呼び出し

I/o マネージャーによって i/o スタックの場所が IRP に追加されるので、 [*Evtdevicewdmiの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)前処理コールバック[**関数は、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) [**ioskip% entiに**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)よって、次の i/o を設定するために ioskipにする必要があります。[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)を呼び出す前の、IRP 内のスタック位置)。

ドライバーが irp を前処理していても IRP を後処理していない場合、ドライバーは、次のコード例に示すように、IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定する必要はなく、 [**Ioskip"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出すことができます。

```cpp
NTSTATUS
  EvtDeviceMyIrpPreprocess(
    IN WDFDEVICE Device,
    IN OUT PIRP Irp
    )
{
//
// Perform IRP preprocessing operations here.
//
...
//
// Deliver the IRP back to the framework. 
//
IoSkipCurrentIrpStackLocation(Irp);
return WdfDeviceWdmDispatchPreprocessedIrp(Device, Irp);
}
```

ドライバーが IRP を再処理する場合、ドライバーは[**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出す必要があります。その後、次のコード例に示すように、 [**iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して、irp の[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定する必要があります。

```cpp
NTSTATUS
  EvtDeviceMyIrpPreprocess(
    IN WDFDEVICE Device,
    IN OUT PIRP Irp
    )
{
//
// Perform IRP preprocessing operations here, if needed.
//
...
//
// Set a completion routine and deliver the IRP back to
// the framework. 
//
IoCopyCurrentIrpStackLocationToNext(Irp);
IoSetCompletionRoutine(
                       Irp,
                       MyIrpCompletionRoutine,
                       NULL,
                       TRUE,
                       TRUE,
                       TRUE
                      );
return WdfDeviceWdmDispatchPreprocessedIrp(Device, Irp);
}
```

ドライバーの[*Evtdevicewdmiの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)前処理コールバック関数が受信したことをデバイスオブジェクトがハンドルした場合、ドライバーは[**Iocopy"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出さないでください (したがって、 [*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定する必要はありません)。物理デバイスオブジェクト (PDO)。 IRP の主要な関数コードが IRP\_MJ\_PNP または IRP\_MJ\_電力。 それ以外の場合、[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)はエラーを報告します。

[**Iocopyを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)呼び出す場合の詳細について[**は、「** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) [Irp をドライバースタックに渡す](https://docs.microsoft.com/windows-hardware/drivers/kernel/passing-irps-down-the-driver-stack)」を参照してください ("irp" を呼び出し[**ます)。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)

 

 






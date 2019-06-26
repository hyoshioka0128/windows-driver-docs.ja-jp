---
title: IRP の前処理と後処理
description: IRP の前処理と後処理
ms.assetid: a0e14ae6-a06e-4c24-8b64-b56f485cf9ff
keywords:
- Irp WDK KMDF の前処理
- 処理後の Irp WDK KMDF
- WDM Irp WDK KMDF、前処理と後処理
- Irp WDK KMDF、前処理と後処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9babfb510d59ef66bd0cc493079c54b7f4f839b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376328"
---
# <a name="preprocessing-and-postprocessing-irps"></a>IRP の前処理と後処理


\[KMDF にのみ適用されます。\]

前に、ドライバーが I/O 要求パケット (IRP) をインターセプトする必要がありますまたはフレームワークは IRP を処理した後、ドライバーを呼び出すことができる場合[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback) を登録する[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)の主要な I/O 関数のコードと、必要に応じて、大規模なコードに関連付けられている特定の小さな I/O 関数コードのイベントのコールバック関数。 その後、フレームワークが、ドライバーの*EvtDeviceWdmIrpPreprocess*ドライバーは、指定されたメジャーおよびマイナーの関数コードを含む IRP を受信するたびに、コールバック関数。

[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数は、IRP の前処理に必要なことすべてを実行できるし、呼び出す必要があります[ **WdfDeviceWdmDispatchPreprocessedIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)をドライバーがない限り、IRP をフレームワークに返す[処理フレームワークがサポートされていない IRP](handling-an-irp-that-the-framework-does-not-support.md)します。

ドライバーの呼び出し後[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)、フレームワーク、ドライバーが指定されていない場合と同じ方法で IRP の処理、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数。 IRP の I/O 関数のコードが、framework がドライバーに渡される 1 つの場合は、ドライバーは IRP がもう一度として受け取ります要求オブジェクト。

ドライバーは、下位レベルのドライバーが IRP、ドライバーが完了したら、IRP の後処理が必要なかどうかは[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数を呼び出すことができます[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を設定する、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンを呼び出す前に[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)します。

ドライバーの呼び出し後[ **WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)、フレームワークが原因で、さらに追加する I/O マネージャー [I/O スタックの場所](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations)すべて Irp をように、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数が設定できる、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。 呼び出す前に、コールバック関数は IRP の I/O スタックの場所のポインターを更新する必要があります[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)します。

### <a name="calling-wdfdevicewdmdispatchpreprocessedirp"></a>Calling WdfDeviceWdmDispatchPreprocessedIrp

I/O マネージャーが、IRP に追加の I/O スタックの場所を追加するため、 [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数を呼び出す必要があります[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)または[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) (IRP の次の I/O スタックの場所を設定する) を呼び出す前に[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)します。

かどうか、ドライバーは IRP、前処理は IRP を後処理いない、ドライバー必要はありませんを設定する、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP の日常的な呼び出すことが[ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)、次のコード例を示しています。

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

ドライバーを呼び出す必要があります、ドライバーは IRP 処理後の場合、 [ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)、呼び出す必要がありますと[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を設定する、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP のルーチンのコード例を次に示します。

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

ドライバーを呼び出してはならない[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) (する必要があります設定しないと、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン) 場合デバイス オブジェクトを処理するドライバーの[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)コールバック関数が表すを受け取る、物理デバイス オブジェクト (PDO) IRP の主要な関数のコードが IRP と\_MJ\_PNP または IRP\_MJ\_電源。 それ以外の場合、 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)エラーをレポートになります。

呼び出すタイミングの詳細については[ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)、 [ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)と[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を参照してください[ドライバー スタックを渡して Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/passing-irps-down-the-driver-stack)します。

 

 






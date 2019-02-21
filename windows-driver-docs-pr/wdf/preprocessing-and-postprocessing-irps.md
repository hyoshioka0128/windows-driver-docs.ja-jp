---
title: 前処理と後処理 Irp
description: 前処理と後処理 Irp
ms.assetid: a0e14ae6-a06e-4c24-8b64-b56f485cf9ff
keywords:
- Irp WDK KMDF の前処理
- 処理後の Irp WDK KMDF
- WDM Irp WDK KMDF、前処理と後処理
- Irp WDK KMDF、前処理と後処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d01f64a404e9698a37009c69ef2506674cb8542
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552882"
---
# <a name="preprocessing-and-postprocessing-irps"></a>前処理と後処理 Irp


\[KMDF にのみ適用されます。\]

前に、ドライバーが I/O 要求パケット (IRP) をインターセプトする必要がありますまたはフレームワークは IRP を処理した後、ドライバーを呼び出すことができる場合[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043) を登録する[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)の主要な I/O 関数のコードと、必要に応じて、大規模なコードに関連付けられている特定の小さな I/O 関数コードのイベントのコールバック関数。 その後、フレームワークが、ドライバーの*EvtDeviceWdmIrpPreprocess*ドライバーは、指定されたメジャーおよびマイナーの関数コードを含む IRP を受信するたびに、コールバック関数。

[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数は、IRP の前処理に必要なことすべてを実行できるし、呼び出す必要があります[ **WdfDeviceWdmDispatchPreprocessedIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546927)をドライバーがない限り、IRP をフレームワークに返す[処理フレームワークがサポートされていない IRP](handling-an-irp-that-the-framework-does-not-support.md)します。

ドライバーの呼び出し後[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)、フレームワーク、ドライバーが指定されていない場合と同じ方法で IRP の処理、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数。 IRP の I/O 関数のコードが、framework がドライバーに渡される 1 つの場合は、ドライバーは IRP がもう一度として受け取ります要求オブジェクト。

ドライバーは、下位レベルのドライバーが IRP、ドライバーが完了したら、IRP の後処理が必要なかどうかは[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数を呼び出すことができます[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)を設定する、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンを呼び出す前に[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)します。

ドライバーの呼び出し後[ **WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546043)、フレームワークが原因で、さらに追加する I/O マネージャー [I/O スタックの場所](https://msdn.microsoft.com/library/windows/hardware/ff551821)すべて Irp をように、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数が設定できる、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。 呼び出す前に、コールバック関数は IRP の I/O スタックの場所のポインターを更新する必要があります[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)します。

### <a name="calling-wdfdevicewdmdispatchpreprocessedirp"></a>Calling WdfDeviceWdmDispatchPreprocessedIrp

I/O マネージャーが、IRP に追加の I/O スタックの場所を追加するため、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数を呼び出す必要があります[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)または[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387) (IRP の次の I/O スタックの場所を設定する) を呼び出す前に[ **WdfDeviceWdmDispatchPreprocessedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff546927)します。

かどうか、ドライバーは IRP、前処理は IRP を後処理いない、ドライバー必要はありませんを設定する、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP の日常的な呼び出すことが[ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)、次のコード例を示しています。

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

ドライバーを呼び出す必要があります、ドライバーは IRP 処理後の場合、 [ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387)、呼び出す必要がありますと[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)を設定する、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP のルーチンのコード例を次に示します。

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

ドライバーを呼び出してはならない[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387) (する必要があります設定しないと、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン) 場合デバイス オブジェクトを処理するドライバーの[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数が表すを受け取る、物理デバイス オブジェクト (PDO) IRP の主要な関数のコードが IRP と\_MJ\_PNP または IRP\_MJ\_電源。 それ以外の場合、 [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)エラーをレポートになります。

呼び出すタイミングの詳細については[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387)、 [ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)と[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)を参照してください[ドライバー スタックを渡して Irp](https://msdn.microsoft.com/library/windows/hardware/ff558781)します。

 

 






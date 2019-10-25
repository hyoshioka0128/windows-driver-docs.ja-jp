---
title: ドライバーによって提供されるスピンロックの使用
description: ドライバーによって提供されるスピンロックの使用
ms.assetid: e81d5c93-47d6-407c-80a2-b2d55f9eb717
keywords:
- スピンロック WDK カーネル
- ドライバーによって提供されるスピンロック WDK カーネル
- グローバルキャンセルスピンロック WDK カーネル
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6105f3989fc60feda8b9d1ceefb8947d97f2cc12
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838367"
---
# <a name="using-a-driver-supplied-spin-lock"></a>ドライバーによって提供されるスピンロックの使用





Irp の独自のキューを管理するドライバーは、システムのキャンセルスピンロックではなく、ドライバーによって提供されるスピンロックを使用して、キューへのアクセスを同期することができます。 本当に必要な場合を除き、キャンセルスピンロックの使用を避けることで、パフォーマンスを向上させることができます。 システムにはキャンセルスピンロックが1つしかないため、ドライバーは、そのスピンロックが使用可能になるまで待機することが必要になる場合があります。 ドライバーによって提供されるスピンロックを使用すると、このような遅延が解消され、i/o マネージャーやその他のドライバーで、キャンセルスピンロックが使用できるようになります。 システムは、ドライバーの[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンを呼び出すときに、キャンセルスピンロックを取得しますが、ドライバーは独自のスピンロックを使用して irp のキューを保護できます。

ドライバーが保留中の Irp をキューに置いていないが、他の方法で所有権を保持している場合でも、そのドライバーは IRP の*キャンセル*ルーチンを設定する必要があり、irp ポインターを保護するにはスピンロックを使用する必要があります。 たとえば、ドライバーが保留中の IRP をマークし、その後、IRP ポインターをコンテキストとして[*Iotimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)ルーチンに渡したとします。 ドライバーは、タイマーをキャンセルする*キャンセル*ルーチンを設定する必要があります。また、IRP にアクセスするときに、*キャンセル*ルーチンとタイマーコールバックの両方で同じスピンロックを使用する必要があります。

独自の Irp をキューに置いて独自のスピンロックを使用するドライバーは、次の操作を行う必要があります。

-   キューを保護するためのスピンロックを作成します。

-   このスピンロックを保持しているときにのみ、*キャンセル*ルーチンを設定してクリアします。

-   ドライバーが IRP をデキューしている間に*キャンセル*ルーチンの実行が開始された場合は、*キャンセル*ルーチンが irp を完了することを許可します。

-   *キャンセル*ルーチンでキューを保護するロックを取得します。

スピンロックを作成するために、ドライバーは[**keinitializer のある Inlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)を呼び出します。 次の例では、ドライバーが、作成したキューと共に**デバイス\_コンテキスト**構造にスピンロックを保存します。

```cpp
typedef struct {
    LIST_ENTRYirpQueue;
    KSPIN_LOCK irpQueueSpinLock;
    ...
} DEVICE_CONTEXT;

VOID InitDeviceContext(DEVICE_CONTEXT *deviceContext)
{
    InitializeListHead(&deviceContext->irpQueue);
    KeInitializeSpinLock(&deviceContext->irpQueueSpinLock);
}
```

IRP をキューに登録するために、ドライバーはスピンロックを取得し、 [**InsertTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-inserttaillist)を呼び出して、次の例のように irp を保留中としてマークします。

```cpp
NTSTATUS QueueIrp(DEVICE_CONTEXT *deviceContext, PIRP Irp)
{
   PDRIVER_CANCEL  oldCancelRoutine;
   KIRQL  oldIrql;
   NTSTATUS  status;

   KeAcquireSpinLock(&deviceContext->irpQueueSpinLock, &oldIrql);

   // Queue the IRP and call IoMarkIrpPending to indicate
   // that the IRP may complete on a different thread.
   // N.B. It is okay to call these inside the spin lock
   // because they are macros, not functions.
   IoMarkIrpPending(Irp);
   InsertTailList(&deviceContext->irpQueue, &Irp->Tail.Overlay.ListEntry);

   // Must set a Cancel routine before checking the Cancel flag.
   oldCancelRoutine = IoSetCancelRoutine(Irp, IrpCancelRoutine);
   ASSERT(oldCancelRoutine == NULL);

   if (Irp->Cancel) {
      // The IRP was canceled. Check whether our cancel routine was called.
      oldCancelRoutine = IoSetCancelRoutine(Irp, NULL);
      if (oldCancelRoutine) {
         // The cancel routine was NOT called.  
         // So dequeue the IRP now and complete it after releasing the spin lock.
         RemoveEntryList(&Irp->Tail.Overlay.ListEntry);
         // Drop the lock before completing the request.
         KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);
         Irp->IoStatus.Status = STATUS_CANCELLED; 
         Irp->IoStatus.Information = 0;
         IoCompleteRequest(Irp, IO_NO_INCREMENT);
         return STATUS_PENDING;

      } else {
         // The Cancel routine WAS called.  
         // As soon as we drop our spin lock, it will dequeue and complete the IRP.
         // So leave the IRP in the queue and otherwise do not touch it.
         // Return pending since we are not completing the IRP here.
         
      }
   }

   KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);

   // Because the driver called IoMarkIrpPending while it held the IRP,
   // it must return STATUS_PENDING from its dispatch routine.
   return STATUS_PENDING;
}
```

この例に示すように、ドライバーは、*キャンセル*ルーチンを設定およびクリアするときに、そのスピンロックを保持します。 サンプルキューのルーチンには、 [**Iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)への2つの呼び出しが含まれています。

最初の呼び出しでは、IRP の*キャンセル*ルーチンを設定します。 ただし、キュールーチンの実行中に IRP が取り消された可能性があるため、ドライバーは IRP の**Cancel**メンバーを確認する必要があります。

-   **Cancel**が設定されている場合は、キャンセルが要求されています。ドライバーは、以前に設定した*キャンセル*ルーチンが呼び出されたかどうかを確認するために、 **iosetcancelroutine**に対して2回目の呼び出しを行う必要があります。

-   IRP がキャンセルされていても、*キャンセル*ルーチンがまだ呼び出されていない場合、現在のルーチンは irp をデキューし、状態\_が取り消された状態で完了します。

-   IRP がキャンセルされ、*キャンセル*ルーチンが既に呼び出されている場合、現在の戻り値は、保留中の irp をマークし、STATUS\_pending を返します。 *Cancel*ルーチンは、IRP を完了します。

次の例は、以前に作成したキューから IRP を削除する方法を示しています。

```cpp
PIRP DequeueIrp(DEVICE_CONTEXT *deviceContext)
{
   KIRQL oldIrql;
   PIRP nextIrp = NULL;

   KeAcquireSpinLock(&deviceContext->irpQueueSpinLock, &oldIrql);

   while (!nextIrp && !IsListEmpty(&deviceContext->irpQueue)) {
      PDRIVER_CANCEL oldCancelRoutine;
      PLIST_ENTRY listEntry = RemoveHeadList(&deviceContext->irpQueue);

      // Get the next IRP off the queue.
      nextIrp = CONTAINING_RECORD(listEntry, IRP, Tail.Overlay.ListEntry);

      // Clear the IRP's cancel routine.
      oldCancelRoutine = IoSetCancelRoutine(nextIrp, NULL);

      // IoCancelIrp() could have just been called on this IRP. What interests us
      // is not whether IoCancelIrp() was called (nextIrp->Cancel flag set), but
      // whether IoCancelIrp() called (or is about to call) our Cancel routine.
      // For that, check the result of the test-and-set macro IoSetCancelRoutine.
      if (oldCancelRoutine) {
         // Cancel routine not called for this IRP. Return this IRP.
         ASSERT(oldCancelRoutine == IrpCancelRoutine);
      } else {
         // This IRP was just canceled and the cancel routine was (or will be)
         // called. The Cancel routine will complete this IRP as soon as we
         // drop the spin lock, so do not do anything with the IRP.
         // Also, the Cancel routine will try to dequeue the IRP, so make 
         // the IRP's ListEntry point to itself.
         ASSERT(nextIrp->Cancel);
         InitializeListHead(&nextIrp->Tail.Overlay.ListEntry);
         nextIrp = NULL;
      }
   }

   KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);

   return nextIrp;
}
```

この例では、ドライバーがキューにアクセスする前に、関連付けられたスピンロックを取得します。 スピンロックを保持しながら、キューが空ではないことを確認し、次の IRP をキューから取得します。 次に、 **Iosetcancelroutine**を呼び出して、IRP の*キャンセル*ルーチンをリセットします。 IRP は、ドライバーが IRP をデキューして*キャンセル*ルーチンをリセットしたときにキャンセルされる可能性があるため、ドライバーは**Iosetcancelroutine**によって返された値を確認する必要があります。 **Iosetcancelroutine**が**NULL**を返した場合は、*キャンセル*ルーチンが呼び出されたか、すぐに呼び出されることを示すために、デキュールーチンは、*キャンセル*ルーチンが IRP を完了できるようにします。 次に、キューを保護するロックを解放し、を返します。

前のルーチンで[**InitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializelisthead)が使用されていることに注意してください。 ドライバーは IRP をキューへして、*キャンセル*ルーチンがデキューできるようにしますが、Irp の**ListEntry**フィールドを再初期化して irp 自体を指すように**InitializeListHead**を呼び出す方が簡単です。 リストの構造は、*キャンセル*ルーチンがスピンロックを取得する前に変更される可能性があるため、自己参照ポインターを使用することが重要です。 また、リストの構造が変更され、 **ListEntry**の元の値が無効になっている場合は、 *CANCEL*ルーチンが IRP のデキュー時にリストを破損する可能性があります。 ただし、 **ListEntry**が irp 自体を指している場合、 *Cancel*ルーチンは常に正しい irp を使用します。

さらに、*キャンセル*ルーチンは次の処理を実行します。

```cpp
VOID IrpCancelRoutine(IN PDEVICE_OBJECT DeviceObject, IN PIRP Irp)
{
   DEVICE_CONTEXT  *deviceContext = DeviceObject->DeviceExtension;
   KIRQL  oldIrql;

   // Release the global cancel spin lock.  
   // Do this while not holding any other spin locks so that we exit at the right IRQL.
   IoReleaseCancelSpinLock(Irp->CancelIrql);

   // Dequeue and complete the IRP.  
   // The enqueue and dequeue functions synchronize properly so that if this cancel routine is called, 
   // the dequeue is safe and only the cancel routine will complete the IRP. Hold the spin lock for the IRP
   // queue while we do this.

   KeAcquireSpinLock(&deviceContext->irpQueueSpinLock, &oldIrql);

   RemoveEntryList(&Irp->Tail.Overlay.ListEntry);

   KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);

   // Complete the IRP. This is a call outside the driver, so all spin locks must be released by this point.
   Irp->IoStatus.Status = STATUS_CANCELLED;
   IoCompleteRequest(Irp, IO_NO_INCREMENT);
   return;
}
```

I/o マネージャーは、*キャンセル*ルーチンを呼び出す前に、常にグローバルキャンセルスピンロックを取得するため、*キャンセル*ルーチンの最初のタスクは、このスピンロックを解放することです。 次に、ドライバーの Irp のキューを保護するスピンロックを取得し、キューから現在の IRP を削除し、そのスピンロックを解放し、状態\_キャンセルされ、priority boost がないことを示す IRP を完了し、を返します。

スピンロックのキャンセルの詳細については、「 [Windows ドライバーのロジックをキャンセル](https://go.microsoft.com/fwlink/p/?linkid=59531)する」ホワイトペーパーを参照してください。

 

 





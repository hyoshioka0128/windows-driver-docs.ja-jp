---
title: ドライバーによって提供されるスピン ロックを使用します。
description: ドライバーによって提供されるスピン ロックを使用します。
ms.assetid: e81d5c93-47d6-407c-80a2-b2d55f9eb717
keywords:
- スピン ロック WDK カーネル
- ドライバーによって提供されるスピン ロック WDK カーネル
- グローバル キャンセル スピン ロック WDK カーネル
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: e50c3cd59e785402dab067d3b648c8ad72d40f3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560049"
---
# <a name="using-a-driver-supplied-spin-lock"></a>ドライバーによって提供されるスピン ロックを使用します。





Irp の独自のキューを管理するドライバーはドライバーによって提供されるスピン ロックを使用して、システムではなく、キューへのアクセスを同期する、スピン ロックをキャンセルできます。 どうしても必要な場合を除くキャンセル スピン ロックの使用を回避することでパフォーマンスを向上できます。 システムが 1 つだけのキャンセル スピン ロックしているため、ドライバーが使用可能になる場合は、そのスピン ロックを待機する必要がある場合があります。 ドライバーによって提供されるスピン ロックを使用して、この潜在的な遅延を排除し、I/O マネージャーとその他のドライバーのキャンセル スピン ロックを使用します。 システムは、ドライバーを呼び出すときにもキャンセル スピン ロックを獲得が[*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742) 、日常的なドライバーを使用して、独自のスピン ロック、Irp のキューを保護します。

ドライバーは Irp、保留キューに登録しませんが、他の方法で所有権を保持、場合でも、そのドライバーが設定する必要があります、*キャンセル*IRP の日常的な IRP のポインターを保護するために、スピン ロックを使用する必要があります。 たとえば、ドライバーは保留中、IRP をマークし、コンテキストとして IRP のポインターを渡します、 [ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)ルーチン。 ドライバーを設定する必要があります、*キャンセル*ルーチンをタイマーをキャンセルし、両方で同じスピン ロックを使用する必要があります、*キャンセル*ルーチンと IRP にアクセスするときは、タイマー コールバック。

独自の Irp のキュー、スピン ロックを使用して、任意のドライバーは、次の方法する必要があります。

-   キューを保護するために、スピン ロックを作成します。

-   設定および解除、*キャンセル*このスピン ロックを保持している場合にのみルーチン。

-   場合、*キャンセル*、ドライバーは IRP をキューから削除中を実行するルーチンを開始できるように、*キャンセル*IRP を完了するルーチン。

-   キューを保護するロックの取得、*キャンセル*ルーチン。

ドライバーの呼び出し、スピン ロックを作成する[ **KeInitializeSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff552160)します。 次の例では、ドライバーがでスピン ロックを保存、**デバイス\_コンテキスト**構造が作成されたキューと共に。

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

スピン ロック、呼び出しを取得するドライバーは IRP をキューに[ **InsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff547823)、次の例のように、保留中、IRP をマークします。

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

ドライバーでは、設定し、クリア中に、スピン ロックが保持している、例に示すように、*キャンセル*ルーチン。 キューのルーチン例にはには、2 つの呼び出しが含まれています。 [ **IoSetCancelRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549674)します。

最初の呼び出しのセット、*キャンセル*IRP のルーチンです。 ただし、キューのルーチンの実行中に IRP が取り消された可能性がありますが、ので、ドライバー チェックする必要があります、**キャンセル**IRP のメンバー。

-   場合**キャンセル**が設定された場合、キャンセルが要求されているし、ドライバーは、2 番目の呼び出しを行う必要があります**IoSetCancelRoutine**表示するかどうか、以前に設定*キャンセル*ルーチンが呼び出されました。

-   IRP が取り消された場合は、*キャンセル*ルーチンが呼び出されていない場合、現在のルーチンは IRP をデキュー状態が完了したら、その\_キャンセルします。

-   IRP が取り消された場合、*キャンセル*ルーチンは既に呼び出されていますが、その後、現在の戻り値は、保留中の IRP をマークし、ステータスを返します\_保留します。 *キャンセル*ルーチンは IRP を完了します。

次の例では、以前に作成したキューから IRP を削除する方法を示します。

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

      // Clear the IRP&#39;s cancel routine.
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
         // the IRP&#39;s ListEntry point to itself.
         ASSERT(nextIrp->Cancel);
         InitializeListHead(&nextIrp->Tail.Overlay.ListEntry);
         nextIrp = NULL;
      }
   }

   KeReleaseSpinLock(&deviceContext->irpQueueSpinLock, oldIrql);

   return nextIrp;
}
```

例では、キューにアクセスする前に、ドライバーが関連付けられているスピン ロックを取得します。 スピン ロックを保持しているときにキューが空でないし、キューから [次へ] の IRP の取得を確認します。 呼び出して**IoSetCancelRoutine**をリセットする、*キャンセル*IRP のルーチンです。 ドライバーは IRP をデキューし、リセット中に、IRP を取り消すことができたので、*キャンセル*、日常的なドライバーはによって返される値を確認する必要があります**IoSetCancelRoutine**します。 場合**IoSetCancelRoutine**返します**NULL**、ことを示します、*キャンセル*デキュー ルーチンにより、しルーチンがされているか、すぐに呼び出されます*キャンセル*ルーチンが IRP を完了します。 キューを保護し、返すロックを解放します。

使用に注意してください[ **InitializeListHead** ](https://msdn.microsoft.com/library/windows/hardware/ff547799)前のルーチンでします。 ドライバーは IRP を入れるでしたように、*キャンセル*ルーチンによってデキューできますが、呼び出す方が簡単です**InitializeListHead**、IRP の再初期化する**ListEntry**フィールドが IRP 自体を指すようにします。 前に、リストの構造を変更する可能性がありますので、重要なは自己参照型のポインターを使用して、*キャンセル*ルーチンは、スピン ロックを取得します。 リスト構造が変更された場合の元の値を行う可能性があると**ListEntry** 、無効な*キャンセル*IRP をデキューするときは、ルーチンに一覧が壊れている可能性があります。 場合**ListEntry**自体、IRP を指す、*キャンセル*ルーチンは、常に正しい IRP を使用します。

*キャンセル*ルーチン、さらに、単には次の処理します。

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

I/O マネージャーは、呼び出す前に常にグローバル キャンセル スピン ロックを取得、*キャンセル*ルーチン、ため、最初のタスクの*キャンセル*ルーチンは、このスピン ロックを解放します。 Irp のドライバーのキューは、保護、キューから現在の IRP を削除、スピン ロックを解放、ステータスの IRP が完了すると、スピン ロックを獲得し\_キャンセルとなしの優先度を向上させることを返します。

キャンセル スピン ロックについての詳細については、次を参照してください。、 [Windows ドライバーでのキャンセル ロジック](https://go.microsoft.com/fwlink/p/?linkid=59531)ホワイト ペーパー。

 

 





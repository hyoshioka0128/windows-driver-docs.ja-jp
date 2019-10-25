---
title: 同期ドライバー通知の処理
description: 同期ドライバー通知の処理
ms.assetid: 84e4e05f-1383-4f5f-8fc0-20cd508afa3c
keywords:
- ドライバー通知 WDK 動的ハードウェアのパーティション分割, 処理
- 同期ドライバー通知 WDK 動的ハードウェアのパーティション分割、処理
- ドライバー通知に登録する WDK 動的ハードウェアパーティション分割、同期
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df7358ac0a555f22d87c67e2db8baad27a66e088
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838489"
---
# <a name="processing-a-synchronous-driver-notification"></a>同期ドライバー通知の処理


オペレーティングシステムは、登録されているコールバック関数を呼び出すと、 [**KE\_\_プロセッサ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_ke_processor_change_notify_context)へのポインターを渡します。これにより、 *changecontext*パラメーターで\_コンテキスト構造を通知\_、変数へのポインターが*Operationstatus*パラメーターに NTSTATUS コードが含まれています。 **KE\_プロセッサ\_変更\_通知\_コンテキスト**構造には、プロセッサの追加操作の状態、追加される新しいプロセッサのプロセッサ番号、およびに関連付けられている NTSTATUS コードが含まれています。指定された状態。

新しいプロセッサがハードウェアパーティションに追加されると、オペレーティングシステムは、登録されているコールバック関数を2回呼び出します。 オペレーティングシステムは、新しいプロセッサを開始する前に、まず**Keprocessoraddstartnotify**状態でコールバック関数を呼び出します。 オペレーティングシステムが新しいプロセッサを正常に追加すると、 **KeProcessorAddCompleteNotify**状態でコールバック関数が2回呼び出されます。 それ以外の場合は、 **KeProcessorAddFailureNotify**状態でコールバック関数をもう一度呼び出します。

デバイスドライバーによってコールバック関数が登録されたときに、KE\_プロセッサ\_CHANGE\_\_既存のフラグが指定されていた場合、コールバック関数は、現在に存在するアクティブな各プロセッサについても、ハードウェアパーティション。 通常、コールバック関数は、既存のプロセッサに対して呼び出される場合と、新しいプロセッサに対して呼び出される場合を区別する必要がありません。 オペレーティングシステムが登録されているコールバック関数を呼び出す場合の詳細については、 [**KeRegisterProcessorChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterprocessorchangecallback)関数の説明を参照してください。

次のコード例は、同期ドライバー通知を処理するコールバック関数の実装を示しています。

```cpp
// Synchronous notification callback function
VOID
  SyncProcessorCallback(
    IN PVOID CallbackContext,
    IN PKE_PROCESSOR_CHANGE_NOTIFICATION_CONTEXT ChangeContext,
    IN PNTSTATUS OperationStatus
    )
{
  PNTSTATUS CallbackStatus;
  ULONG ProcessorNumber;
  ULONG ProcessorCount;
  KAFFINITY ActiveProcessors;

  // The CallbackContext contains a pointer to a
  // variable that contains an NTSTATUS code. This
  // is used to pass back any error status to the
  // caller of KeRegisterProcessorChangeCallback.
  CallbackStatus =
    (PNTSTATUS)
      CallbackContext;

  // Get the processor number of the new processor
  ProcessorNumber =
    ChangeContext->NtNumber;

  // Switch on the state of the add operation
  switch (ChangeContext->State)
  {
    // Before the operating system has added the new processor
    case KeProcessorAddStartNotify:

      // Allocate any per-processor data
      // structures for the new processor.
      ...

      // Assign any other per-processor resources
      // to the new processor.
      ...

      // Perform any other necessary preparation
      // for execution of the driver code
      // on the new processor.
      ...

      // If an error occurs such that continuing
      // to add the processor would be fatal
      // (for example, an allocation failure of a
      // per-processor data structure), set the
      // status to an appropriate NTSTATUS code.
      if (...)
      {
        // This returns the status to the operating system.
        *OperationStatus = STATUS_INSUFFICIENT_RESOURCES;

        // This returns the status to the caller of the
        // KeRegisterProcessorChangeCallback function.
        *CallbackStatus = STATUS_INSUFFICIENT_RESOURCES;
      }

      break;

    // The operating system has successfully added the new processor
    case KeProcessorAddCompleteNotify:

      //
      // The following can be performed either here or
      // in an asynchronous notification callback function.
      //

      // Get the current processor count and affinity
      ProcessorCount =
        KeQueryActiveProcessorCount(
          &ActiveProcessors
          );

      // Adjust any resource allocations that are based
      // on the number of processors.
      ...

      // Adjust the assignment of resources that are
      // assigned to specific processors.
      ...

      // Begin scheduling any per-processor threads
      // on the new processor.
      ...

      // Adjust the scheduling of DPCs and other threads
      ...

      // Adjust any load balancing algorithms
      ...

      break;

    // The operating system has failed to add the new processor
    case KeProcessorAddFailureNotify:

      // Clean up and free any per-processor
      // resources that were allocated for the
      // specified processor during the
      // KeProcessorAddStartNotify state.
      ...

      break;
  }
}
```

 

 





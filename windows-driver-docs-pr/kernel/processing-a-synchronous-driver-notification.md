---
title: 同期ドライバー通知の処理
description: 同期ドライバー通知の処理
ms.assetid: 84e4e05f-1383-4f5f-8fc0-20cd508afa3c
keywords:
- ドライバーの通知の WDK が動的なハードウェア パーティション分割、処理
- ドライバーの同期の通知の WDK が動的なハードウェア パーティション分割、処理
- ドライバー WDK の動的なハードウェア パーティション分割、同期の通知に登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c51bf91d66e5eee3bfebee22a8c976ae22e7620
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570765"
---
# <a name="processing-a-synchronous-driver-notification"></a>同期ドライバー通知の処理


ポインターを渡す、オペレーティング システムに登録されたコールバック関数を呼び出すと、 [ **KE\_プロセッサ\_変更\_通知\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff554229)構造体、 *ChangeContext*でコードをパラメーターと、NTSTATUS を格納する変数へのポインター、 *OperationStatus*パラメーター。 **KE\_プロセッサ\_変更\_通知\_コンテキスト**構造体には、プロセッサの状態が含まれています追加操作は、追加される新しいプロセッサのプロセッサ数。指定された状態に関連付けられている NTSTATUS コード。

新しいプロセッサがハードウェアのパーティションに追加されると、オペレーティング システムは 2 回に登録されたコールバック関数を呼び出します。 オペレーティング システムが最初使用して、コールバック関数を呼び出す、 **KeProcessorAddStartNotify**状態の新しいプロセッサを開始する前にします。 2 回目にコールバック関数を呼び出してオペレーティング システムは、新しいプロセッサを正常に追加する場合、 **KeProcessorAddCompleteNotify**状態。 コールバック関数を呼び出し、それ以外の場合、2 回目に、 **KeProcessorAddFailureNotify**状態。

場合、KE\_プロセッサ\_変更\_追加\_デバイス ドライバーには、コールバック関数が登録されているときに、既存のフラグが指定された、アクティブな各プロセッサのコールバック関数が直ちに呼び出さもを現在、ハードウェアのパーティションに存在します。 通常、コールバック関数は、既存のプロセッサと、新しいプロセッサで呼び出されたときに呼び出された場合に区別するためにはありません。 詳細については、オペレーティング システムが登録されたコールバック関数を呼び出すの説明を参照して、 [ **KeRegisterProcessorChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff553120)関数。

次のコード例では、ドライバーの同期の通知を処理するコールバック関数の実装を示しています。

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

 

 





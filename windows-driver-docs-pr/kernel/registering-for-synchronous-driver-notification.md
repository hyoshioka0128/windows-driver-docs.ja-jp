---
title: 同期ドライバー通知登録
description: 同期ドライバー通知登録
ms.assetid: 852a2b69-c71f-4127-946e-8179954d504c
keywords:
- ドライバーの通知の WDK が動的なハードウェア パーティション分割、登録します。
- 同期の通知 WDK 動的ハードウェア パーティション分割、登録します。
- 通知 WDK 動的ハードウェア パーティション分割、登録します。
- ドライバーの同期の通知の WDK が動的なハードウェア パーティション分割、登録します。
- ドライバーの通知の WDK の動的なハードウェア パーティショニングの登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f055374a1a700fcffb813076868d625a3425e1e8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350343"
---
# <a name="registering-for-synchronous-driver-notification"></a>同期ドライバー通知登録


ドライバーの同期の通知を使用するには、デバイス ドライバーは、ハードウェア パーティションに新しいプロセッサを動的に追加するときに、オペレーティング システムが呼び出すコールバック関数を実装します。 次のコード例では、このようなコールバック関数のプロトタイプを示します。

```cpp
// Prototype for the synchronous
// notification callback function
VOID
  SyncProcessorCallback(
    IN PVOID CallbackContext,
    IN PKE_PROCESSOR_CHANGE_NOTIFY_CONTEXT ChangeContext,
    IN PNTSTATUS OperationStatus
    );
```

デバイス ドライバーを呼び出すことによって同期ドライバー通知の登録、 [ **KeRegisterProcessorChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff553120)関数。 デバイス ドライバーの通常の呼び出し、 **KeRegisterProcessorChangeCallback**関数内からその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数。 デバイス ドライバーが、キーを指定する場合\_プロセッサ\_変更\_追加\_既存フラグは、現在のハードウェアのパーティションに存在するアクティブな各プロセッサのコールバック関数を呼び出すすぐに新しいプロセッサがハードウェアのパーティションに追加されたときに呼び出されるに追加します。 次のコード例では、ドライバーの同期の通知に登録する方法を示します。

```cpp
PVOID CallbackRegistrationHandle;
NTSTATUS CallbackStatus = STATUS_SUCCESS;

// The driver's DriverEntry routine
NTSTATUS  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  ...

  // Register the callback function
  CallbackRegistrationHandle =
    KeRegisterProcessorChangeCallback(
      SyncProcessorCallback,
      &CallbackStatus,
      KE_PROCESSOR_CHANGE_ADD_EXISTING
      );

  // Check the result
  if (CallbackRegistrationHandle == NULL)
  {
    // Perform any necessary cleanup
    ...

    // Check the callback status
    if (CallbackStatus != STATUS_SUCCESS)
    {
      // Return the error status from the callback function
      return CallbackStatus;
    }
    else
    {
      // Return a generic error status
      return STATUS_UNSUCCESSFUL;
    }
  }

  ...

  return STATUS_SUCCESS;
}
```

ときにデバイス ドライバをする必要がありますの受信を停止ドライバーの同期の通知など、呼び出すことによってコールバック関数を解除する必要がありますアンロードされているときに、 [ **KeDeregisterProcessorChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff552015)関数。 デバイス ドライバーの通常の呼び出し、 **KeDeregisterProcessorChangeCallback**関数内からその[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。 次のコード例では、コールバック関数を登録解除する方法を示します。

```cpp
// The driver's Unload routine
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    );
{
  ...

  // Unregister the callback function
  KeDeregisterProcessorChangeCallback(
    CallbackRegistrationHandle
    );

  ...
}
```

 

 





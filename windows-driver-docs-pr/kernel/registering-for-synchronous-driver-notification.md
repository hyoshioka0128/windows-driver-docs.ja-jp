---
title: 同期ドライバー通知登録
description: 同期ドライバー通知登録
ms.assetid: 852a2b69-c71f-4127-946e-8179954d504c
keywords:
- ドライバー通知 WDK 動的ハードウェアパーティション分割、登録
- 同期通知 WDK 動的ハードウェアのパーティション分割、登録
- 通知 WDK 動的ハードウェアのパーティション分割、登録
- 同期ドライバー通知 WDK 動的ハードウェアパーティション分割、登録
- ドライバー通知の登録 WDK 動的ハードウェアパーティション分割
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78a186b86d56a0f1d1d03336f0dde6821a0eb15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838461"
---
# <a name="registering-for-synchronous-driver-notification"></a>同期ドライバー通知登録


同期ドライバー通知を使用するために、デバイスドライバーは、新しいプロセッサをハードウェアパーティションに動的に追加するときにオペレーティングシステムによって呼び出されるコールバック関数を実装します。 次のコード例は、このようなコールバック関数のプロトタイプです。

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

デバイスドライバーは、 [**KeRegisterProcessorChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterprocessorchangecallback)関数を呼び出すことによって、同期ドライバーの通知を登録します。 通常、デバイスドライバーは[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数内から**KeRegisterProcessorChangeCallback**関数を呼び出します。 デバイスドライバーで KE\_プロセッサが指定されている場合\_\_既存のフラグを追加\_には、現在ハードウェアパーティションに存在するアクティブな各プロセッサに対して、コールバック関数が呼び出されます。新しいプロセッサがハードウェアパーティションに追加されたとき。 次のコード例は、同期ドライバー通知を登録する方法を示しています。

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

デバイスドライバーが、アンロード中などの同期ドライバーの通知の受信を停止する必要がある場合は、 [**KeDeregisterProcessorChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterprocessorchangecallback)関数を呼び出すことによって、コールバック関数の登録を解除する必要があります。 通常、デバイスドライバーは、 [*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数内から**KeDeregisterProcessorChangeCallback**関数を呼び出します。 次のコード例は、コールバック関数の登録を解除する方法を示しています。

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

 

 





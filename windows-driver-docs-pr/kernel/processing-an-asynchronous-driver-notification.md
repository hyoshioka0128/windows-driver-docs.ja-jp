---
title: 非同期ドライバー通知の処理
description: 非同期ドライバー通知の処理
ms.assetid: 7e7ed971-5891-4b91-909a-1e140b764fed
keywords:
- ドライバーの通知の WDK が動的なハードウェア パーティション分割、処理
- ドライバーの非同期通知の WDK が動的なハードウェア パーティション分割、処理
- ドライバー WDK の動的なハードウェア パーティション分割、非同期の通知に登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a926e447e2ce368943e3ce6342b20f1a28f145
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378815"
---
# <a name="processing-an-asynchronous-driver-notification"></a>非同期ドライバー通知の処理


ポインターを渡す、オペレーティング システムに登録されたコールバック関数を呼び出すと、 [**デバイス\_インターフェイス\_変更\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_interface_change_notification)構造体、*NotificationStructure*パラメーター。

次のコード例では、プロセッサのドライバーが非同期通知を処理するコールバック関数の実装を示しています。

```cpp
// Asynchronous processor notification callback function
NTSTATUS
  AsyncProcessorCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    )
{
  PDEVICE_INTERFACE_CHANGE_NOTIFICATION Notification;
  ULONG ProcessorCount;
  KAFFINITY ActiveProcessors;

  Notification = 
    (PDEVICE_INTERFACE_CHANGE_NOTIFICATION)
      NotificationStructure;

  // Verify that this notification is about a processor
  // that is being added to the hardware partition.
  if (IsEqualGUID(
        &Notification->Event,
        &GUID_DEVICE_INTERFACE_ARRIVAL
        ))
  {
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

    // Begin scheduling any per processor threads
    // on the new processor.
    ...

    // Adjust the scheduling of DPCs and other threads
    ...

    // Adjust any load balancing algorithms
    ...
  }

  // Always return success status
 return STATUS_SUCCESS;
}
```

次のコード例では、メモリのドライバーが非同期通知を処理するコールバック関数の実装を示しています。

```cpp
// Asynchronous memory notification callback function
NTSTATUS
  AsyncMemoryCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    )
{
  PDEVICE_INTERFACE_CHANGE_NOTIFICATION Notification;

  Notification = 
    (PDEVICE_INTERFACE_CHANGE_NOTIFICATION)
      NotificationStructure;

  // Verify that this notification is about memory
  // that is being added to the hardware partition.
  if (IsEqualGUID(
        &Notification->Event,
        &GUID_DEVICE_INTERFACE_ARRIVAL
        ))
  {
    // Increase the size of any memory buffers
    // for optimal performance of the driver.
    ...
  }

  // Always return success status
  return STATUS_SUCCESS;
}
```

 

 





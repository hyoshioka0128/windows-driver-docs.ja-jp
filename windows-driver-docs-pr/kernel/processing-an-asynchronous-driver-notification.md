---
title: 非同期ドライバー通知の処理
description: 非同期ドライバー通知の処理
ms.assetid: 7e7ed971-5891-4b91-909a-1e140b764fed
keywords:
- ドライバー通知 WDK 動的ハードウェアのパーティション分割, 処理
- 非同期ドライバー通知 WDK 動的ハードウェアのパーティション分割、処理
- ドライバー通知に登録する WDK 動的ハードウェアパーティション分割、非同期
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef4ced4edbab7e150342cfd600db011b2c187d50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838487"
---
# <a name="processing-an-asynchronous-driver-notification"></a>非同期ドライバー通知の処理


オペレーティングシステムは、登録されているコールバック関数を呼び出すと、デバイス\_インターフェイスへのポインターを渡し、 *notificationstructure*パラメーターの[**通知構造\_変更\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_interface_change_notification)ます。

次のコード例は、プロセッサの非同期ドライバー通知を処理するコールバック関数の実装を示しています。

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

次のコード例は、メモリの非同期ドライバー通知を処理するコールバック関数の実装を示しています。

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

 

 





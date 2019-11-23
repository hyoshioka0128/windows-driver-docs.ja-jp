---
title: 非同期ドライバー通知登録
description: 非同期ドライバー通知登録
ms.assetid: e1f97a65-7c82-4d7b-97ec-0293fc69fd8c
keywords:
- ドライバー通知 WDK 動的ハードウェアパーティション分割、登録
- 非同期通知 WDK 動的ハードウェアパーティション分割
- 通知 WDK 動的ハードウェアのパーティション分割、登録
- 非同期ドライバー通知 WDK 動的ハードウェアパーティション分割、登録
- ドライバー通知の登録 WDK 動的ハードウェアパーティション分割
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6439c3de8468bbe9aab944dab5188f1d2adeb6d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838465"
---
# <a name="registering-for-asynchronous-driver-notification"></a>非同期ドライバー通知登録


非同期ドライバー通知を使用するために、デバイスドライバーは、プロセッサまたはメモリモジュールをハードウェアパーティションに動的に追加するときに、オペレーティングシステムが呼び出すコールバック関数を実装します。 次のコード例は、このようなコールバック関数のプロトタイプを示しています。

```cpp
// Prototypes for the asynchronous
// notification callback functions
NTSTATUS
  AsyncProcessorCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    );

NTSTATUS
  AsyncMemoryCallback(
    IN PVOID NotificationStructure,
    IN PVOID Context
    );
```

デバイスドライバーは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)関数を呼び出して非同期通知を登録します。各デバイスドライバーのコールバック関数では、 *eventカテゴリデータ*パラメーターの次の guid のいずれかへのポインターを指定します。

<a href="" id="guid-device-processor"></a>GUID\_デバイス\_プロセッサ  
プロセッサがハードウェアパーティションに動的に追加されたときに通知されるように登録します。

<a href="" id="guid-device-memory"></a>GUID\_デバイス\_メモリ  
メモリがハードウェアパーティションに動的に追加されたときに通知されるように登録します。

これらの Guid は、ヘッダーファイルの Poclass に定義されています。

次のコード例は、両方の通知に登録する方法を示しています。

```cpp
PVOID ProcessorNotificationEntry;
PVOID MemoryNotificationEntry;
NTSTATUS Status;

Status =
  IoRegisterPlugPlayNotification(
    EventCategoryDeviceInterfaceChange,
    0,
    &GUID_DEVICE_PROCESSOR,
    DriverObject,
    AsyncProcessorCallback,
    NULL,
    &ProcessorNotificationEntry
    );

Status =
  IoRegisterPlugPlayNotification(
    EventCategoryDeviceInterfaceChange,
    0,
    &GUID_DEVICE_MEMORY,
    DriverObject,
    AsyncMemoryCallback,
    NULL,
    &MemoryNotificationEntry
    );
```

**注**   デバイスドライバーにプロセッサに関する通知のみを行う必要がある場合は、メモリのコールバック関数を実装したり、メモリに関する通知を登録したりする必要はありません。 同様に、デバイスドライバーにメモリに関する通知のみを行う必要がある場合は、プロセッサのコールバック関数を実装したり、プロセッサに関する通知を受け取るように登録したりする必要はありません。

 

デバイスドライバーが、アンロード中などの非同期ドライバー通知の受信を停止する必要がある場合は、 [**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)関数を呼び出すことによって、各コールバック関数の登録を解除する必要があります。 次のコード例は、コールバック関数の登録を解除する方法を示しています。

```cpp
// Unregister for asynchronous notifications
Status =
  IoUnregisterPlugPlayNotification(
    ProcessorNotificationEntry
    );

Status =
  IoUnregisterPlugPlayNotification(
    MemoryNotificationEntry
    );
```

 

 





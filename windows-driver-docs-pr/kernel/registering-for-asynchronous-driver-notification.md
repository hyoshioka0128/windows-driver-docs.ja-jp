---
title: ドライバーの非同期通知を登録します。
description: ドライバーの非同期通知を登録します。
ms.assetid: e1f97a65-7c82-4d7b-97ec-0293fc69fd8c
keywords:
- ドライバーの通知の WDK が動的なハードウェア パーティション分割、登録します。
- WDK の動的なハードウェア パーティショニングの非同期通知
- 通知 WDK 動的ハードウェア パーティション分割、登録します。
- ドライバーの非同期通知の WDK が動的なハードウェア パーティション分割、登録します。
- ドライバーの通知の WDK の動的なハードウェア パーティショニングの登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d6c2de67b4a1094cc4779e72e6ec5d16270fb1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552456"
---
# <a name="registering-for-asynchronous-driver-notification"></a>ドライバーの非同期通知を登録します。


ドライバーの非同期通知を使用してデバイス ドライバーでは、オペレーティング システムが動的に追加すると、プロセッサやメモリ モジュール ハードウェア パーティションに呼び出すコールバック関数が実装されています。 次のコード例では、このようなコールバック関数のプロトタイプを示しています。

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

デバイス ドライバーを呼び出して非同期通知の登録、 [ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526)関数は、1 回の各デバイス ドライバーのコールバック関数、ポインターを指定します。対応する Guid の次のいずれかに、 *EventCategoryData*パラメーター。

<a href="" id="guid-device-processor"></a>GUID\_デバイス\_プロセッサ  
プロセッサがハードウェアのパーティションに動的に追加されたときに通知に登録します。

<a href="" id="guid-device-memory"></a>GUID\_デバイス\_メモリ  
ハードウェア パーティションにメモリが動的に追加される通知に登録します。

これらの Guid は、ヘッダー ファイル、Poclass.h で定義されます。

次のコード例では、両方の通知に登録する方法を示します。

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

**注**  にされている場合、デバイス ドライバーのみプロセッサに関する通知を受けることはありませんメモリのコールバック関数を実装またはメモリについての通知に登録します。 同様に、デバイス ドライバーは、メモリに関する通知を受けるのみがないプロセッサ用のコールバック関数を実装またはプロセッサについての通知に登録します。

 

ときにデバイス ドライバーする必要がありますの受信を停止、ドライバーが非同期通知など、呼び出すことによって各コールバック関数を解除する必要がありますアンロードされているときに、 [ **IoUnregisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550398)関数。 次のコード例では、コールバック関数を登録解除する方法を示します。

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

 

 





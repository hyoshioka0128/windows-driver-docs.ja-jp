---
title: アプリケーション通知を登録します。
description: アプリケーション通知を登録します。
ms.assetid: e8f76014-6068-4012-96c6-88ea2bbd9bbf
keywords:
- 動的なハードウェアの WDK、アプリケーション通知をパーティション分割
- ハードウェアの WDK、動的なアプリケーションの通知をパーティション分割
- パーティションの WDK 動的のハードウェア、アプリケーションの通知
- アプリケーション通知の WDK が動的なハードウェア パーティション分割、登録します。
- 通知 WDK の動的なハードウェアが、アプリケーションのパーティション分割
- アプリケーション通知 WDK 動的ハードウェア パーティション分割の登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca5090ac42fd425954f185c1956b0ef29a0114be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550825"
---
# <a name="registering-for-application-notification"></a>アプリケーション通知を登録します。


ユーザー モード アプリケーションを呼び出す、 [RegisterDeviceNotification](https://go.microsoft.com/fwlink/p/?linkid=97892)自体と、プロセッサやメモリのモジュールがハードウェアのパーティションに動的に追加されたときに通知を登録する関数。 アプリケーションを呼び出す、 **RegisterDeviceNotification**関数では、プロセッサのイベントの通知を登録する 1 つの時間とメモリ イベントの通知に登録する 2 番目の時間を 2 回です。 これらのイベントの通知を登録する際に、アプリケーションは次の Guid のいずれかを指定します。

<a href="" id="guid-device-processor"></a>GUID\_デバイス\_プロセッサ  
プロセッサがハードウェアのパーティションに動的に追加されたときに通知を受けるアプリケーションを登録します。

<a href="" id="guid-device-memory"></a>GUID\_デバイス\_メモリ  
メモリがハードウェアのパーティションに動的に追加されたときに通知を受けるアプリケーションを登録します。

これらの Guid は、ヘッダー ファイル、Poclass.h で定義されます。

次のコード例では、両方の通知に登録する方法を示します。

```cpp
HWND hWnd;
DEV_BROADCAST_DEVICEINTERFACE ProcessorFilter;
DEV_BROADCAST_DEVICEINTERFACE MemoryFilter;
HDEVNOTIFY ProcessorNotifyHandle;
HDEVNOTIFY MemoryNotifyHandle;

// The following example assumes that hWnd already
// contains a handle to the application window that
// is to receive the WM_DEVICECHANGE messages.

// Initialize the filter for processor event notification
ZeroMemory(
  &ProcessorFilter,
  sizeof(ProcessorFilter)
  );
ProcessorFilter.dbcc_size =
  sizeof(DEV_BROADCAST_DEVICEINTERFACE);
ProcessorFilter.dbcc_devicetype =
  DBT_DEVTYP_DEVICEINTERFACE;
ProcessorFilter.dbcc_classguid =
  GUID_DEVICE_PROCESSOR;

// Register the application window to receive
// WM_DEVICECHANGE messages for processor events.
ProcessorNotifyHandle =
  RegisterDeviceNotification(
    hWnd,
    &ProcessorFilter,
    DEVICE_NOTIFY_WINDOW_HANDLE
    );

// Initialize the filter for memory event notification
ZeroMemory(
  &MemoryFilter,
  sizeof(MemoryFilter)
  );
MemoryFilter.dbcc_size =
  sizeof(DEV_BROADCAST_DEVICEINTERFACE);
MemoryFilter.dbcc_devicetype =
  DBT_DEVTYP_DEVICEINTERFACE;
MemoryFilter.dbcc_classguid =
  GUID_DEVICE_MEMORY;

// Register the application&#39;s window to receive
// WM_DEVICECHANGE messages for memory events.
MemoryNotifyHandle =
  RegisterDeviceNotification(
    hWnd,
    &MemoryFilter,
    DEVICE_NOTIFY_WINDOW_HANDLE
    );
```

**注**  アプリケーションは、プロセッサに関する通知を受けるのみがないメモリ イベントの通知を登録します。 同様に、アプリケーションは、メモリに関する通知を受けるのみがないプロセッサ イベントの通知を登録します。

 

WM の受信からウィンドウを登録解除できますプロセッサまたはメモリ イベントの通知を受信するアプリケーションが不要になったの\_DEVICECHANGE メッセージを呼び出すことによってこれらのイベントを[UnregisterDeviceNotification](https://go.microsoft.com/fwlink/p/?linkid=97893)関数。 次のコード例では、アプリケーション通知の登録を解除する方法を示します。

```cpp
// Unregister the application window from receiving
// WM_DEVICECHANGE messages for processor events.
UnregisterDeviceNotification(ProcessorNotifyHandle);

// Unregister the application window from receiving
// WM_DEVICECHANGE messages for memory events.
UnregisterDeviceNotification(MemoryNotifyHandle);
```

詳細については、 **RegisterDeviceNotification**と**UnregisterDeviceNotification**関数の場合は、Microsoft Windows SDK ドキュメントを参照してください。

 

 





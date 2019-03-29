---
title: ハードウェア エラー イベントの通知登録
description: ハードウェア エラー イベントの通知登録
ms.assetid: 86816fc7-fa69-4ecf-9d50-822b0fa6992d
keywords:
- イベント通知の登録の WDK WHEA
- ハードウェア イベント通知を登録します。
- WDK WHEA の通知
- WHEA WDK、イベント通知を登録します。
- イベント通知を登録する、Windows ハードウェア エラー アーキテクチャ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab7fc5a19fdfade3d64daaae0bc842057080e641
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571683"
---
# <a name="registering-for-notification-of-hardware-error-events"></a>ハードウェア エラー イベントの通知登録


新しいハードウェアのエラー イベントに関する通知を受けるを登録するには、アプリケーションは、WHEA プロバイダーによって発行されるすべてのイベントへのサブスクリプションを作成します。 WHEA のプロバイダーの名前は**Microsoft Windows カーネル WHEA**します。

WHEA プロバイダーを先には、ハードウェアのエラー イベントを発生させるチャネルは次のとおりです。

-   **システム**チャネル (Windows Vista の場合)。

-   **Microsoft Windows カーネル WHEA**チャネル (Windows Server 2008 および Windows Vista SP1)。

-   **Microsoft-Windows のカーネルの WHEA/エラー**チャネル (Windows 7 およびそれ以降のバージョン)。

### <a name="windows-vista"></a>Windows Vista

次のコード例では、このバージョンの Windows の新しいハードウェア エラー イベントの通知に登録する方法を示します。

```cpp
// Prototype for the notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  );

// Function to create a subscription to all hardware error
// events that are raised by the WHEA provider.
EVT_HANDLE SubscribeHwErrorEvents(VOID)
{
  EVT_HANDLE SubHandle;

  // Create a subscription to all events that are sent to
  // the System channel by the WHEA provider.
  SubHandle =
    EvtSubscribe(
      NULL,
      NULL,
      L"System", 
      L"*[System/Provider[@Name=\"Microsoft-Windows-Kernel-WHEA\"]]",
      NULL,
      NULL,
      HwErrorEventCallback,
      EvtSubscribeToFutureEvents
      );

   // Return the subscription handle
   return SubHandle;
}

// Notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  )
{
  // Check the action
  if (Action == EvtSubscribeActionDeliver) {

    // Process the hardware error event
    ProcessHwErrorEvent(EventHandle);
  }

  // Return success status
  return ERROR_SUCCESS;
}

// Function to terminate the subscription
VOID UnsubscribeHwErrorEvents(EVT_HANDLE SubHandle)
{
  // Close the subscription handle
  EvtClose(SubHandle);
}
```

### <a name="windows-server-2008-windows-vista-sp1-and-later-versions"></a>Windows Server 2008、Windows Vista SP1 およびそれ以降のバージョン

次のコード例では、これらのバージョンの Windows の新しいハードウェア エラー イベントの通知に登録する方法を示します。

```cpp
// Prototype for the notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  );

// Function to create a subscription to all hardware error
// events that are raised by the WHEA provider.
EVT_HANDLE SubscribeHwErrorEvents(VOID)
{
  EVT_HANDLE SubHandle;

  // Create a subscription to all events that are sent
  // to the WHEA channel.
#if (WINVER <= _WIN32_WINNT_LONGHORN)
  SubHandle =
    EvtSubscribe(
      NULL,
      NULL,
      L"Microsoft-Windows-Kernel-WHEA", 
      L"*",
      NULL,
      NULL,
      HwErrorEventCallback,
      EvtSubscribeToFutureEvents
      );
#else
  SubHandle =
    EvtSubscribe(
      NULL,
      NULL,
      L" Microsoft-Windows-Kernel-WHEA/Errors", 
      L"*",
      NULL,
      NULL,
      HwErrorEventCallback,
      EvtSubscribeToFutureEvents
      );
#endif

   // Return the subscription handle
   return SubHandle;
}

// Notification callback function
DWORD WINAPI HwErrorEventCallback(
  EVT_SUBSCRIBE_NOTIFY_ACTION Action,
  PVOID Context,
  EVT_HANDLE EventHandle
  )
{
  // Check the action
  if (Action == EvtSubscribeActionDeliver) {

    // Process the hardware error event
    ProcessHwErrorEvent(EventHandle);
  }

  // Return success status
  return ERROR_SUCCESS;
}

// Function to terminate the subscription
VOID UnsubscribeHwErrorEvents(EVT_HANDLE SubHandle)
{
  // Close the subscription handle
  EvtClose(SubHandle);
}
```

**注**  のすべて、 **Evt * Xxx*** 関数と、EVT\_*XXX*に前の例で使用されていたデータ型が記載されている、 [Windows イベント ログ](https://go.microsoft.com/fwlink/p/?linkid=81187)Microsoft Windows SDK のドキュメント セクション。

 

 

 





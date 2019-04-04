---
title: アプリケーション通知の処理
description: アプリケーション通知の処理
ms.assetid: 475d8e37-5d31-4989-92ce-3c4a7c09d292
keywords:
- 動的なハードウェアの WDK、アプリケーション通知をパーティション分割
- ハードウェアの WDK、動的なアプリケーションの通知をパーティション分割
- パーティションの WDK 動的のハードウェア、アプリケーションの通知
- アプリケーション通知の WDK が動的なハードウェア パーティション分割、登録します。
- 通知 WDK の動的なハードウェアが、アプリケーションのパーティション分割
- アプリケーション通知 WDK 動的ハードウェア パーティション分割の登録
- アプリケーション通知 WDK のハードウェアの動的パーティションの処理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 676df98a2afb890a539e348a2b5e7b3a8c493c1c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348657"
---
# <a name="processing-an-application-notification"></a>アプリケーション通知の処理


ユーザー モード アプリケーションが WM をどのように処理するか\_DEVICECHANGE メッセージは、アプリケーションを Win32 API に基づいているか、または Microsoft Foundation Class (MFC) ライブラリに基づいているかどうかによって異なります。

### <a name="win32-applications"></a>Win32 アプリケーション

Win32 ベースのアプリケーションが実装することによって、アプリケーションのウィンドウに送信されるメッセージを処理する*ウィンドウ プロシージャ*します。 ウィンドウ プロシージャの詳細については、、[ウィンドウ プロシージャ](https://go.microsoft.com/fwlink/p/?linkid=96748)、Microsoft Windows SDK ドキュメントのトピックを参照してください。

次のコード例は、WM を処理する方法を示しています。\_Win32 ベースのアプリケーションで DEVICECHANGE メッセージ。

```cpp
// Prototype for the function that handles the
// processing of WM_DEVICECHANGE messages.
LRESULT
OnDeviceChange(
  WPARAM wParam,
  LPARAM lParam
  ); 

// The application's message processing function
// for the window that receives the WM_DEVICECHANGE
// messages.
LRESULT CALLBACK
WindowProc(
  HWND hWnd,
  UINT uMsg,
  WPARAM wParam,
  LPARAM lParam
  )
{
  switch (uMsg)
  {
      .
      .  // Cases for other messages
      .
    // Device change message
    case WM_DEVICECHANGE:
      OnDeviceChange(wParam, lParam);
      break;
      .
      .  // Cases for other messages
      .
    // Catchall for all messages that are
    // not handled by the application.
    default:
      return DefWindowProc(
               hWnd,
               uMsg,
               wParam,
               lParam
               );
  }

  return 0;
}

// The function that handles the processing
// of WM_DEVICECHANGE messages.
LRESULT
OnDeviceChange(
  WPARAM wParam,
  LPARAM lParam
  )
{
  PDEV_BROADCAST_HDR devHdr;
  PDEV_BROADCAST_DEVICEINTERFACE devInterface;
  HANDLE ProcessHandle;
  DWORD_PTR ProcessAffinityMask;
  DWORD_PTR SystemAffinityMask;
  DWORD_PTR ChangedAffinityMask;
  MEMORYSTATUSEX MemoryStatus;

  // Check whether the message is a device arrival message
  if (wParam == DBT_DEVICEARRIVAL)
  {
    // Get a pointer to the structure header
    devHdr = (PDEV_BROADCAST_HDR)lParam;

    // Check whether the message is about a device interface
    if (devHdr->dbch_devicetype == DBT_DEVTYP_DEVICEINTERFACE)
    {
      // Get a pointer to the device interface structure
      devInterface = (PDEV_BROADCAST_INTERFACE)devHdr;

      // Check whether this is a message about a processor
      if (IsEqualGUID(
            devInterface->dbcc_classguid,
            GUID_DEVICE_PROCESSOR
            ))
      {
        // Get a handle to the current process
        ProcessHandle =
          GetCurrentProcess();

        // Get the current process and system affinity masks
        GetProcessAffinityMask(
          ProcessHandle,
          &ProcessAffinityMask,
          &SystemAffinityMask
          );

        // Get a mask of any change to the set of processors
        ChangedAffinityMask =
          ProcessAffinityMask ^ SystemAffinityMask;

        // Perform any per processor memory allocation
        // for any new processors
        ...

        // Set the process affinity mask to use all the
        // active processors in the hardware partition.
        SetProcessAffinityMask(
          ProcessHandle,
          SystemAffinityMask
          );

        // Adjust the number of threads in any thread
        // pools as needed for optimal performance.
        ...
      }

      // Check whether this is a message about memory
      else if (IsEqualGUID(
                 devInterface->dbcc_classguid,
                 GUID_DEVICE_MEMORY
                 ))
      {
        // Get the current memory status
        GlobalMemoryStatusEx(&MemoryStatus);

        // Note: MemoryStatus.ullTotalPhys contains
        // the amount of physical memory in the
        // hardware partition.

        // Adjust the memory buffer allocations
        // as needed for optimal performance.
        ...
      }
    }
  }

  return 0;
}
```

### <a name="mfc-applications"></a>MFC アプリケーション

MFC フレームワークは、MFC ベースのアプリケーションのウィンドウに送信されるメッセージを処理します。 MFC ベースのアプリケーションを実装する必要があります、 [OnDeviceChange](https://go.microsoft.com/fwlink/p/?linkid=97894) 、WM を受信するアプリケーションのウィンドウ クラスのメンバー関数\_DEVICECHANGE メッセージ。

次のコード例は、実装する方法を示します、 **OnDeviceChange** MFC ベースのアプリケーションでのメンバー関数。

```cpp
afx_msg BOOL
CAppWnd::OnDeviceChange(
  UINT nEventType,
  DWORD_PTR dwData
  )
{
  PDEV_BROADCAST_HDR devHdr;
  PDEV_BROADCAST_DEVICEINTERFACE devInterface;
  HANDLE ProcessHandle;
  DWORD_PTR ProcessAffinityMask;
  DWORD_PTR SystemAffinityMask;
  DWORD_PTR ChangedAffinityMask;
  MEMORYSTATUSEX MemoryStatus;

  if (nEventType == DBT_DEVICEARRIVAL)
  {
    devHdr = (PDEV_BROADCAST_HDR)dwData;

    if (devHdr->dbch_devicetype == DBT_DEVTYP_DEVICEINTERFACE)
    {
      devInterface = (PDEV_BROADCAST_INTERFACE)devHdr;

      if (IsEqualGUID(
            devInterface->dbcc_classguid,
            GUID_DEVICE_PROCESSOR
            ))
      {
        // Get a handle to the current process
        ProcessHandle =
          GetCurrentProcess();

        // Get the current process and system affinity masks
        GetProcessAffinityMask(
          ProcessHandle,
          &ProcessAffinityMask,
          &SystemAffinityMask
          );

        // Get a mask of any change to the set of processors
        ChangedAffinityMask =
          ProcessAffinityMask ^ SystemAffinityMask;

        // Perform any per processor memory allocation
        // for the new processors
        ...

        // Set the process affinity mask to use all the
        // active processors in the hardware partition.
        SetProcessAffinityMask(
          ProcessHandle,
          SystemAffinityMask
          );

        // Adjust the number of threads in any thread
        // pools as needed for optimal performance.
        ...
      }
      else if (IsEqualGUID(
                 devInterface->dbcc_classguid,
                 GUID_DEVICE_MEMORY
                 ))
      {
        // Get the current memory status
        GlobalMemoryStatusEx(&MemoryStatus);

        // Note: MemoryStatus.ullTotalPhys contains
        // the amount of physical memory in the
        // hardware partition.

        // Adjust the memory buffer allocations
        // as needed for optimal performance.
        ...
      }
    }
  }

  return TRUE;
}
```

 

 





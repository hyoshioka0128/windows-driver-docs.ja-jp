---
title: ハードウェア エラー イベントに対するシステム イベント ログの照会
description: ハードウェア エラー イベントに対するシステム イベント ログの照会
ms.assetid: e2290a1b-6fde-4843-9c52-17279f93a887
keywords:
- イベント WDK WHEA、システム イベント ログのクエリを実行します。
- WDK WHEA のシステム イベント ログのクエリを実行します。
- WDK WHEA ログに記録します。
- WHEA WDK、システム イベント ログのクエリを実行します。
- システム イベント ログのクエリを実行する、Windows ハードウェア エラー アーキテクチャ WDK
- イベント ログ WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1788b6db8a6e6af67f789f582fb5a21a7fe77322
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581458"
---
# <a name="querying-the-system-event-log-for-hardware-error-events"></a>ハードウェア エラー イベントに対するシステム イベント ログの照会


ハードウェア エラーのイベント ログに記録するプロバイダーの名前は次のとおりです。

-   **Microsoft Windows カーネル WHEA** (Windows Vista の場合)。

-   **Microsoft Windows WHEA ロガー** (Windows Server 2008、Windows Vista SP1 およびそれ以降のバージョン)。

### <a name="windows-vista"></a>Windows Vista

次のコード例では、WHEA によってログに記録された以前のハードウェア エラー イベントを取得する、システム イベント ログを照会する方法を示します。

```cpp
// Function to query the event log for hardware error events
VOID QueryHwErrorEvents(VOID) {

  EVT_HANDLE QueryHandle;
  EVT_HANDLE EventHandle;
  ULONG Returned;

  // Obtain a query handle to the system event log
  QueryHandle =
    EvtQuery(
      NULL, 
      L"System", 
      L"*[System/Provider[@Name=\"Microsoft-Windows-Kernel-WHEA\"]]",
      EvtQueryChannelPath | EvtQueryForwardDirection
      );

  // Check result
  if (QueryHandle != NULL) {

    // Get the next hardware error event
    while (EvtNext(
             QueryHandle,
             1,
             &EventHandle,
             -1,
             0,
             &Returned
             )) {

      // Process the hardware error event
      ProcessHwErrorEvent(EventHandle);

      // Close the event handle
      EvtClose(EventHandle);
    }

    // Close the query handle
    EvtClose(QueryHandle);
  }
}
```

### <a name="windows-server-2008-windows-vista-sp1-and-later-versions"></a>Windows Server 2008、Windows Vista SP1 およびそれ以降のバージョン

次のコード例では、WHEA によってログに記録された以前のハードウェア エラー イベントを取得する、システム イベント ログを照会する方法を示します。

```cpp
// Function to query the event log for hardware error events
VOID QueryHwErrorEvents(VOID) {

  EVT_HANDLE QueryHandle;
  EVT_HANDLE EventHandle;
  ULONG Returned;

  // Obtain a query handle to the system event log
  QueryHandle =
    EvtQuery(
      NULL, 
      L"System", 
      L"*[System/Provider[@Name=\"Microsoft-Windows-WHEA-Logger\"]]",
      EvtQueryChannelPath | EvtQueryForwardDirection
      );

  // Check result
  if (QueryHandle != NULL) {

    // Get the next hardware error event
    while (EvtNext(
             QueryHandle,
             1,
             &EventHandle,
             -1,
             0,
             &Returned
             )) {

      // Process the hardware error event
      ProcessHwErrorEvent(EventHandle);

      // Close the event handle
      EvtClose(EventHandle);
    }

    // Close the query handle
    EvtClose(QueryHandle);
  }
}
```

**注**  のすべて、 **Evt * Xxx*** 関数と、EVT\_*XXX*に前の例で使用されていたデータ型が記載されている、 [Windows イベント ログ](https://go.microsoft.com/fwlink/p/?linkid=81187)Microsoft Windows SDK のドキュメント セクション。

 

 

 





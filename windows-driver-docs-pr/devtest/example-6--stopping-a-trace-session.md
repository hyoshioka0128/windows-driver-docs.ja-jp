---
title: 例 6 のトレース セッションを停止します。
description: 例 6 のトレース セッションを停止します。
ms.assetid: a8520531-bebb-4334-9dc3-d50f4a851e7e
keywords:
- トレース セッションを停止する WDK
- トレース セッションを停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aef4eae6325a2827594a5626d98ec15dadb60d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558695"
---
# <a name="example-6-stopping-a-trace-session"></a>例 6:トレース セッションを停止します。


## <span id="ddk_stopping_a_trace_session_tools"></span><span id="DDK_STOPPING_A_TRACE_SESSION_TOOLS"></span>


次のコマンドは、MyTrace トレース セッションを停止します。

```
tracelog -stop MyTrace
```

応答では、トレース ログは、トレース セッションのプロパティを表示します。

```
Operation Status:       0L      The operation completed successfully.

Logger Name:            MyTrace
Logger Id:              2
Logger Thread Id:       000008C8
Buffer Size:            8 Kb
Maximum Buffers:        26
Minimum Buffers:        4
Number of Buffers:      6
Free Buffers:           6
Buffers Written:        1
Events Lost:            0
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Log Filename:           C:\Tracing\MyTrace.etl
```

トレース セッションが停止したことを確認するには、リストを使用 (**tracelog-l**) またはクエリ (**tracelog q**) コマンド。

 

 






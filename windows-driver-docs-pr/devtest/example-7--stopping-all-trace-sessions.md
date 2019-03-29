---
title: 例 7 のすべてのトレース セッションを停止しています
description: 例 7 のすべてのトレース セッションを停止しています
ms.assetid: a832bf9a-ab7e-4ec0-823b-52bc6016e791
keywords:
- トレース セッションを停止する WDK
- トレース セッションを停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c19fe1e8a954a13b53d52624539d6a1202dca99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582478"
---
# <a name="example-7-stopping-all-trace-sessions"></a>例 7:すべてのトレース セッションの停止


## <span id="ddk_stopping_all_trace_sessions_tools"></span><span id="DDK_STOPPING_ALL_TRACE_SESSIONS_TOOLS"></span>


次のコマンドは、コンピューターのすべてのトレース セッションを停止します。

```
tracelog -x
```

応答でトレース ログ、コンピューターで実行されている各トレース セッションの一覧し、のセッションを停止するかどうかを尋ねます。 以下に例を示します。

```
Do you want to stop the "My Trace" session (Y or N)?
```

セッションを停止するには、次のように入力します。 **Y**します。トレース ログは、次のメッセージとセッションのプロパティを示します。

```
The "MyTrace" session has been stopped
```

 

 






---
title: リアルタイムのトレース セッションを開始する 10 の使用例
description: リアルタイムのトレース セッションを開始する 10 の使用例
ms.assetid: 1dfa8cf1-dd51-4415-b6d4-84241db2aa03
keywords:
- WDK、リアルタイムのトレース セッション
- WDK のリアルタイムのトレース セッション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d205ea49f63df5fcaa187f88995061aac3df90f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560596"
---
# <a name="example-10-starting-a-real-time-trace-session"></a>例 10:リアルタイムのトレース セッションを開始します。


## <span id="ddk_starting_a_real_time_trace_session_tools"></span><span id="DDK_STARTING_A_REAL_TIME_TRACE_SESSION_TOOLS"></span>


次のコマンドは、- リアルタイムのトレース セッションを開始、セッションのトレース メッセージがログ ファイルに送信されるのではなくトレース コンシューマーに直接送信されます。

```
tracelog -start MyTrace guid MyProvider.guid -rt
```

これらのログ ファイルに影響を与えるパラメーターを除き、トレースのログ セッションを使用するリアルタイムのトレース セッションをカスタマイズするのにのと同じパラメーターを使用できます。 これには、特殊なトレース セッションとプライベートのトレース セッションのトレースをリアルタイムに含まれます。 ただし、トレース ログがあるため、[トレース コント ローラー](trace-controller.md)ではなく、[トレース コンシューマー](trace-consumer.md)、トレース ログを使用して、リアルタイムのトレース セッション中に生成されたトレース メッセージを表示することはできません。 代わりに、トレース コンシューマーをなど使用[Tracefmt](tracefmt.md)を使用して、または[traceview で](traceview.md)、トレース コント ローラーとトレース コンシューマーの両方であります。

次のコマンドは、MyTrace リアルタイム トレース セッションからのトレース メッセージを書式設定する、コマンド プロンプト ウィンドウに表示を調べる場合は後でテキスト ファイルに保存 Tracefmt を使用します。 コマンドの構文の詳細については、次を参照してください。 [Tracefmt](tracefmt.md)します。

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

 

 






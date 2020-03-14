---
title: トレース セッション
description: トレース セッション
ms.assetid: 50a8cc64-5127-4abe-a6a8-514ca5db63ab
keywords:
- トレースセッション WDK
- トレースセッション WDK、トレースセッションについて
- セッション WDK ソフトウェアのトレース
- プライベートトレースセッション WDK
- バッファーされるトレースセッション WDK
- リアルタイムトレースセッション WDK
- トレースログセッション WDK
- ユーザーモードのトレースセッション WDK
- トレースセッションのプロセス WDK
- 予約済みのトレースセッション WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8007a394639abeb3d5382ab7aaa13222958d62eb
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79243015"
---
# <a name="trace-session"></a>トレース セッション


## <span id="ddk_trace_session_tools"></span><span id="DDK_TRACE_SESSION_TOOLS"></span>


トレース*セッション*は、トレース[プロバイダー](trace-provider.md)がトレースメッセージを生成する期間です。 トレースセッションがトレース[ログ](trace-log.md)または[トレースコンシューマー](trace-consumer.md)に配信 ("フラッシュ") されるまで、トレースメッセージを格納するためのバッファーのセットがシステムによって保持されます。

トレースセッションには、トレースログセッション、リアルタイムトレースセッション、バッファリングされたトレースセッションの3種類があります。 1つのトレースセッションには、トレースログセッション、リアルタイムトレースセッション、またはその両方を指定できます。 バッファーされたトレースセッションは排他的です。

さらに、プライベートトレースセッションや、 [NT カーネルロガートレース](nt-kernel-logger-trace-session.md)セッションや[グローバルロガートレースセッション](global-logger-trace-session.md)などの予約済みのトレースセッションがあります。これは、ログセッションまたはリアルタイムセッションとして実行できます。 標準ツールを使用すると、これらのセッションを制御し、結果のトレースメッセージを表示できます。

### <a name="span-idddk_trace_log_sessions_toolsspanspan-idddk_trace_log_sessions_toolsspantrace-log-sessions"></a><span id="ddk_trace_log_sessions_tools"></span><span id="DDK_TRACE_LOG_SESSIONS_TOOLS"></span>トレースログセッション

トレース*ログセッション*では、トレースメッセージは、トレースバッファーからバイナリ形式でログファイルに書き込まれます。 これは、標準の既定のトレースセッションの種類です。

### <a name="span-idddk_real_time_trace_sessions_toolsspanspan-idddk_real_time_trace_sessions_toolsspanreal-time-trace-sessions"></a><span id="ddk_real_time_trace_sessions_tools"></span><span id="DDK_REAL_TIME_TRACE_SESSIONS_TOOLS"></span>リアルタイムトレースセッション

*リアルタイムのトレースセッション*では、トレースメッセージは、ログファイルに送信されるのではなく、 [Traceview](traceview.md)や[tracefmt](tracefmt.md)などのトレースコンシューマーに直接配信されます。

### <a name="span-idddk_buffered_trace_sessions_toolsspanspan-idddk_buffered_trace_sessions_toolsspanbuffered-trace-sessions"></a><span id="ddk_buffered_trace_sessions_tools"></span><span id="DDK_BUFFERED_TRACE_SESSIONS_TOOLS"></span>バッファーされるトレースセッション

バッファーされた*トレースセッション*では、トレースメッセージはトレースバッファーに残ります。[トレースログ](trace-log.md)に書き込まれたり、[トレースコンシューマー](trace-consumer.md)に配信されたりすることはありません。 バッファーは、循環ファイルと同じように保持されます。 いっぱいになると、最新のトレースメッセージによってバッファー内の最も古いトレースメッセージが上書きされます。

バッファーされたトレースセッションは、Windows Vista 以降のバージョンの Windows でのみサポートされます。

一般に、ソフトウェアのトレースではオーバーヘッドはほとんど発生しませんが、バッファリングされたトレースセッションでは、すべての種類のトレースセッションのオーバーヘッドが最小限に抑えられます。 長期間トレースして、興味深い問題が発生した場合は、デバッガーを使用して現在のバッファーの内容を調べたり、現在のバッファーの内容をトレースログに保存したりできます。

トレースバッファー内のトレースメッセージを表示するには、 **! wmitrace**の特殊化されたデバッガー拡張機能を使用します。 この拡張機能の詳細については、「 *Windows 用デバッグツール*」を参照してください。

バッファーの内容を[トレースログ](trace-log.md)にフラッシュするには、**トレースログ-flush**コマンドの **-f**パラメーターを使用します。

バッファーされたトレースセッションを開始するには、**トレースログ-start**コマンドの **-バッファリング**パラメーターを使用します。 詳細については、「 [**Tracelog コマンドの構文**](tracelog-command-syntax.md)」を参照してください。

### <a name="span-idddk_private_trace_sessions_toolsspanspan-idddk_private_trace_sessions_toolsspanprivate-trace-sessions"></a><span id="ddk_private_trace_sessions_tools"></span><span id="DDK_PRIVATE_TRACE_SESSIONS_TOOLS"></span>プライベートトレースセッション

*プライベートトレースセッション*は、ユーザーモードでトレースするユーザーモードプロセスの一部として実行されるトレースセッションです。 (標準のトレースセッションはカーネルで実行されます)。プライベートトレースセッションは、*ユーザーモードのトレース*セッションまたは*プロセストレースセッション*とも呼ばれます。

複数のプライベートトレースセッションを同時に実行することはできますが、各プロセスで実行できるプライベートトレースセッションは1つだけです。

プライベートトレースセッションのリアルタイムトレースを実行することはできません。 トレースメッセージをログに書き込む必要があります。

プライベートトレースセッションで使用されるバッファーは、常にページング可能です。 これらのバッファーには、ページングメモリまたは非ページメモリを指定できません。

トレースメッセージをプライベートトレースセッションからデバッガーに送信することはできません。 WMI トレース拡張機能 ( **! wmitrace**) では、プライベートトレースセッションはサポートされていません。

プライベートイベントのトレースセッションの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 






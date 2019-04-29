---
title: トレース セッション
description: トレース セッション
ms.assetid: 50a8cc64-5127-4abe-a6a8-514ca5db63ab
keywords:
- WDK のトレース セッション
- トレース セッションの詳細については、トレース セッション WDK、
- セッションの WDK ソフトウェア トレース
- WDK のプライベート トレース セッション
- WDK のバッファー内のトレース セッション
- WDK のリアルタイムのトレース セッション
- WDK のトレース ログ セッション
- ユーザー モード トレース セッション WDK
- WDK のトレース セッションを処理します。
- WDK の予約済みのトレース セッション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8007a394639abeb3d5382ab7aaa13222958d62eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392693"
---
# <a name="trace-session"></a>トレース セッション


## <span id="ddk_trace_session_tools"></span><span id="DDK_TRACE_SESSION_TOOLS"></span>


A*トレース セッション*は、期間、[トレース プロバイダー](trace-provider.md)トレース メッセージを生成します。 システムでは、一連のトレース セッション (「フラッシュされた」) が配信されるまで、トレース メッセージを保存するバッファーを維持する、[トレース ログ](trace-log.md)または[トレース コンシューマー](trace-consumer.md)します。

トレース セッションの 3 つの基本的な種類があります。 トレース ログ セッション、リアルタイムのトレース セッション、およびバッファー内のトレース セッション。 1 つのトレース セッション トレースのログ セッション、リアルタイムのトレース セッションの場合、またはその両方を使用できます。 バッファー内のトレース セッションは排他的です。

さらに、あるプライベート トレース セッションと予約済みのトレース セッションをなど、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)と[グローバル ロガー トレース セッション](global-logger-trace-session.md)、ログ セッションとして実行またはリアルタイムセッションです。 これらのセッションを制御し、結果のトレース メッセージを表示するのには、標準のツールを使用できます。

### <a name="span-idddktracelogsessionstoolsspanspan-idddktracelogsessionstoolsspantrace-log-sessions"></a><span id="ddk_trace_log_sessions_tools"></span><span id="DDK_TRACE_LOG_SESSIONS_TOOLS"></span>ログのトレース セッション

*トレース ログ セッション*、トレース メッセージは、トレース バッファーからバイナリ形式でログ ファイルに書き込まれます。 これは、標準的な既定のトレース セッションの種類です。

### <a name="span-idddkrealtimetracesessionstoolsspanspan-idddkrealtimetracesessionstoolsspanreal-time-trace-sessions"></a><span id="ddk_real_time_trace_sessions_tools"></span><span id="DDK_REAL_TIME_TRACE_SESSIONS_TOOLS"></span>リアルタイムのトレース セッション

*リアルタイム トレース セッション*、トレース メッセージがなどのトレース コンシューマーに直接配信される[traceview で](traceview.md)または[Tracefmt](tracefmt.md)の代わりに、または、に加えて、送信されます。ログ ファイル。

### <a name="span-idddkbufferedtracesessionstoolsspanspan-idddkbufferedtracesessionstoolsspanbuffered-trace-sessions"></a><span id="ddk_buffered_trace_sessions_tools"></span><span id="DDK_BUFFERED_TRACE_SESSIONS_TOOLS"></span>バッファー内のトレース セッション

*トレース セッションのバッファー*、トレース メッセージ トレース バッファーに残ります。 には書き込まれません、[トレース ログ](trace-log.md)に配信または、[トレース コンシューマー](trace-consumer.md)します。 バッファーは循環ファイルのように維持されます。 完全なは、最新のトレース メッセージはバッファー内の最も古いトレース メッセージを上書きします。

バッファー内のトレース セッションは、Windows Vista および Windows の以降のバージョンでのみサポートされます。

ソフトウェア トレース、一般に、非常にわずかなオーバーヘッドが発生した場合はバッファー内のトレース セッションはすべてのトレース セッションの種類の最小限のオーバーヘッドがあります。 長期間にトレースすることができ、次に、興味深い問題が発生した場合、デバッガーを使用して、現在のバッファーの内容を確認したり、トレース ログの現在のバッファーの内容を保存します。

トレース バッファー内のトレース メッセージを表示する、 **! wmitrace**デバッガー拡張機能を特殊化します。 この拡張機能については、次を参照してください。*ツールを Windows のデバッグ*します。

コンテンツ バッファーのフラッシュ、[トレース ログ](trace-log.md)を使用して、 **-f**のパラメーター、 **tracelog-フラッシュ**コマンド。

バッファー内のトレース セッションを開始するには、使用、 **-バッファリング**のパラメーター、 **tracelog-開始**コマンド。 詳細については、次を参照してください。 [ **Tracelog コマンド構文**](tracelog-command-syntax.md)します。

### <a name="span-idddkprivatetracesessionstoolsspanspan-idddkprivatetracesessionstoolsspanprivate-trace-sessions"></a><span id="ddk_private_trace_sessions_tools"></span><span id="DDK_PRIVATE_TRACE_SESSIONS_TOOLS"></span>プライベート トレース セッション

A*プライベート トレース セッション*はそれを追跡するユーザー モード プロセスの一環として、ユーザー モードで実行されているトレース セッションです。 (標準のトレース セッションは、カーネルで実行)。プライベートのトレース セッションとも呼ばれます*ユーザー モード トレース セッション*または*トレース セッションを処理*します。

一度に 1 つ以上のプライベート トレース セッションを実行できますが、プロセスごとに 1 つだけのプライベート トレース セッションを実行することができます。

プライベートのトレース セッションのトレースをリアルタイムで行うことはできません。 トレース メッセージは、ログに書き込ま 必要があります。

プライベート トレース セッションで使用されるバッファーは、ページングは常にします。 これらのバッファー ページまたは非ページ メモリを指定することはできません。

デバッガーをプライベートのトレース セッションからのトレース メッセージを送信できません。 WMI のトレース拡張機能 (**! wmitrace**) は、プライベートのトレース セッションをサポートしていません。

プライベート イベント トレース セッションの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 






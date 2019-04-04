---
title: ソフトウェア トレース ツールのアンケート
description: ソフトウェア トレース ツールのアンケート
ms.assetid: d6b5d131-ed03-4961-9680-1c4ded35de96
keywords:
- ソフトウェアが示されているツールを WDK のトレース
- トレース WDK、記載されているツール
- トレースの追加
- トレースの WDK、ソフトウェアの追加
- WDK、トレースを追加します。
- WDK のトレース、セッションを制御するソフトウェア
- トレース セッションを制御する WDK
- ソフトウェアは、WDK をトレース TMF ファイル
- トレースの WDK、TMF ファイル
- ソフトウェアの WDK のトレース、メッセージの書式設定
- メッセージの書式設定、WDK のトレース
- WDK のトレース、メッセージを表示するソフトウェア
- トレース メッセージを表示する WDK
- WDK のトレース、イベントを表示するソフトウェア
- イベントの表示、WDK のトレース
- トレース コンシューマ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b61d157a36319926691e98acba80ca3e2bb05e74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551911"
---
# <a name="survey-of-software-tracing-tools"></a>ソフトウェア トレース ツールのアンケート


## <span id="ddk_survey_of_software_tracing_tools_tools"></span><span id="DDK_SURVEY_OF_SOFTWARE_TRACING_TOOLS_TOOLS"></span>


Windows Driver Kit (WDK) または Windows オペレーティング システムのいずれかでは、次のソフトウェア トレース ツールが含まれます。

### <a name="span-idenablingwpptracinginatraceproducerspanspan-idenablingwpptracinginatraceproducerspanenabling-wpp-tracing-in-a-trace-producer"></a><span id="enabling_wpp__tracing_in_a_trace_producer"></span><span id="ENABLING_WPP__TRACING_IN_A_TRACE_PRODUCER"></span>トレースのプロデューサーで WPP トレースを有効にします。

-   TraceWPP (TraceWPP.exe) のソース ファイルで、Windows ソフトウェア トレース プリプロセッサ (WPP) を実行するコマンド ライン ツールは、[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーまたはユーザー モード アプリケーションなどです。

    TraceWPP では、ドライバーまたは WDK と Visual Studio を使用してアプリケーションをビルドするときに、WPP オプションを設定する代わりに提供します。 このツールのプロセスでは、ソース ファイル内のマクロをトレースし、WPP トレースを有効にするヘッダー ファイルを作成します。

    際に使用されるものと同じ TraceWPP のコマンド ライン オプションは、 [TraceWPP タスク](tracewpp-task.md)は MSBuild に渡されます。 これらのオプションの詳細については、[WPP プリプロセッサ](wpp-preprocessor.md)を参照してください。

    TraceWPP が、箱にある\\&lt;*プラットフォーム*&gt; WDK のディレクトリ。

### <a name="span-idcontrollingtracesessionstracecontrollersspanspan-idcontrollingtracesessionstracecontrollersspancontrolling-trace-sessions-trace-controllers"></a><span id="controlling_trace_sessions__trace_controllers_"></span><span id="CONTROLLING_TRACE_SESSIONS__TRACE_CONTROLLERS_"></span>(トレース コント ローラー) のトレース セッションを制御します。

-   [Traceview で](traceview.md)(TraceView.exe) は GUI ベース[トレース コント ローラー](trace-controller.md)と[トレース コンシューマー](trace-consumer.md)とは、トレース メッセージのリアルタイム表示に特に設計されています。 により、構成、開始、更新と停止[トレース セッション](trace-session.md)します。 このツールも書式設定、フィルター、およびリアルタイムのトレース セッションからのトレース メッセージを表示し、[トレース ログ](trace-log.md)します。

    Traceview で結合しの機能が拡張され[Tracepdb](tracepdb.md)、 [Tracelog](tracelog.md)、および[Tracefmt](tracefmt.md)します。 詳しくは、開始 traceview でとの間、**ヘルプ**] メニューの [選択**ヘルプ トピック**します。

    Traceview では、ツールである\\&lt;*プラットフォーム*&gt; 、WDK のサブディレクトリで&lt;*プラットフォーム*&gt;は x86 または x64 のいずれか。

-   [Tracelog](tracelog.md) (Tracelog.exe) は、コマンド ライン[トレース コント ローラー](trace-controller.md)をによりでを構成します、開始、更新、およびリアルタイムを停止しますファイルとログ セッション。 トレース ログは、ユーザー モードとカーネル モードのトレース セッションをサポートしているだけでなく[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)と[グローバル ロガー (ブート) のトレース セッション](global-logger-trace-session.md)します。 このツールが遅延プロシージャに費やされた時間を測定するトレースをサポートしても呼び出し (Dpc) および割り込みサービス ルーチン (Isr)。

    トレース ログは、ツールにある\\&lt;*プラットフォーム*&gt; 、WDK のサブディレクトリで&lt;*プラットフォーム*&gt;は x86 または x64 のいずれか。

-   Logman (Logman.exe) が完全に機能を GUI ベース[トレース コント ローラー](trace-controller.md)はパフォーマンス カウンターおよびイベント トレースのログ記録を制御するために特に設計されています。

    Windows XP および Windows の以降のバージョンので Logman が含まれます。 このツールを使用する方法の詳細については、、 [Logman](https://go.microsoft.com/fwlink/p/?linkid=179385) TechNet web サイトのトピックを参照してください。

### <a name="span-idcreatingtmffilesspanspan-idcreatingtmffilesspancreating-tmf-files"></a><span id="creating_tmf_files"></span><span id="CREATING_TMF_FILES"></span>TMF ファイルを作成します。

-   [Tracepdb](tracepdb.md) (Tracepdb.exe) が作成するコマンド ライン サポート ツール[トレース メッセージの形式 (TMF) ファイル](trace-message-format-file.md)トレース メッセージからの指示を書式設定[PDB シンボル ファイル](pdb-symbol-files.md)します。

    トレースのメッセージが表示されるツール[Tracefmt](tracefmt.md)(Tracefmt.exe) と[traceview で](traceview.md)(TraceView.exe) は書式設定し、トレース メッセージを表示する TMF ファイルから書式設定の手順を使用することができます。

    Tracefmt できますから TMF ファイルを作成しても[PDB シンボル ファイル](pdb-symbol-files.md)します。

    Tracepdb と Tracefmt ツールにある\\トレース\\&lt;*プラットフォーム*&gt; 、WDK のサブディレクトリで&lt;*プラットフォーム*&gt;は x86 または x64 のいずれか。

### <a name="span-idformattinganddisplayingtracemessagestraceconsumersspanspan-idformattinganddisplayingtracemessagestraceconsumersspanformatting-and-displaying-trace-messages-trace-consumers"></a><span id="formatting_and_displaying_trace_messages__trace_consumers_"></span><span id="FORMATTING_AND_DISPLAYING_TRACE_MESSAGES__TRACE_CONSUMERS_"></span>書式設定して、トレース メッセージ (トレース コンシューマー) を表示します。

-   [Tracefmt](tracefmt.md)は、コマンド ライン[トレース コンシューマー](trace-consumer.md)に書式設定*トレース メッセージ*(**TraceMessage**) からのリアルタイムのトレース セッションまたはトレース ログ、および書き込みファイルまたはコマンド プロンプト ウィンドウに表示されます。

-   Tracerpt (Tracerpt.exe) は、コマンド ライン[トレース コンシューマー](trace-consumer.md)に書式設定*トレース イベント*(**TraceEvent**) パフォーマンス カウンターし、CSV または XML ファイルに書き込むとします。 また、イベントを分析し、概要レポートを生成します。

    Tracerpt は、Windows XP および Windows の以降のバージョンに含まれます。 このツールを使用する方法の詳細については、[Tracerpt](https://go.microsoft.com/fwlink/p/?linkid=179389) TechNet web サイトのトピックを参照してください。

-   [Traceview で](traceview.md)、GUI ツール、つまりトレース コント ローラーとトレース コンシューマーも書式設定し、トレース メッセージが表示されます (**TraceMessage**) からのリアルタイムのトレース セッションまたはトレース ログ。 フィルター処理しを参照しやすく、表形式で、トレース メッセージを表示します。

### <a name="span-idviewingtraceeventsinadebuggerspanspan-idviewingtraceeventsinadebuggerspanviewing-trace-events-in-a-debugger"></a><span id="viewing_trace_events_in_a_debugger"></span><span id="VIEWING_TRACE_EVENTS_IN_A_DEBUGGER"></span>デバッガーでのトレース イベントの表示

-   デバッグ ツールの Windows を含む **! wmitrace**、トレース セッションで、トレース メッセージを表示する特殊なデバッガー拡張機能は、ログ ファイルに書き込まれる、または表示用に提供される前にバッファー処理します。

-   [Tracelog](tracelog.md)と[traceview で](traceview.md)KD または Windbg、トレース メッセージをリダイレクトできる方がアタッチされています。 詳細については、トレース ログを参照してください。 **-kd**パラメーターと、traceview で**Windbg**オプション。

### <a name="span-idanalyzingdpcandisrexecutiontimesspanspan-idanalyzingdpcandisrexecutiontimesspananalyzing-dpc-and-isr-execution-times"></a><span id="analyzing_dpc_and_isr_execution_times"></span><span id="ANALYZING_DPC_AND_ISR_EXECUTION_TIMES"></span>DPC と ISR の実行時間の分析

-   Windows XP Service Pack 2 (SP2) 以降で使用できます[Tracelog](tracelog.md)を遅延プロシージャ呼び出し (DPC) のログし NT Kernel Logger のトレース セッションでサービス ルーチン (ISR) イベントを中断または、Tracerpt を使用して、概要レポートの作成ログです。 詳細については、例を含む、このツールを使用する方法の詳細については、トレース ログを参照してください。

 

 






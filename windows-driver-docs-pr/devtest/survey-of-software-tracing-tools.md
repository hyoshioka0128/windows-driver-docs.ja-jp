---
title: ソフトウェア トレース ツールの調査
description: ソフトウェア トレース ツールの調査
ms.assetid: d6b5d131-ed03-4961-9680-1c4ded35de96
keywords:
- ソフトウェアトレース WDK、ツール一覧
- WDK のトレース、ツールの一覧
- トレースの追加
- ソフトウェアトレース WDK、追加
- WDK のトレース、追加
- ソフトウェアのトレース WDK、セッションの制御
- WDK のトレース、セッションの制御
- ソフトウェアトレース WDK、TMF ファイル
- WDK、TMF ファイルのトレース
- ソフトウェアトレース WDK, 書式設定メッセージ
- WDK のトレース, メッセージの書式設定
- ソフトウェアトレース WDK, メッセージの表示
- WDK をトレースし、メッセージを表示する
- ソフトウェアトレース WDK, イベントの表示
- WDK のトレース, イベントの表示
- トレースコンシューマー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2214e4b059c7f5635146eb85124df58928918742
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208888"
---
# <a name="survey-of-software-tracing-tools"></a>ソフトウェア トレース ツールの調査


## <span id="ddk_survey_of_software_tracing_tools_tools"></span><span id="DDK_SURVEY_OF_SOFTWARE_TRACING_TOOLS_TOOLS"></span>


次のソフトウェアトレースツールは、Windows Driver Kit (WDK) または Windows オペレーティングシステムに含まれています。

### <a name="span-idenabling_wpp__tracing_in_a_trace_producerspanspan-idenabling_wpp__tracing_in_a_trace_producerspanenabling-wpp-tracing-in-a-trace-producer"></a><span id="enabling_wpp__tracing_in_a_trace_producer"></span><span id="ENABLING_WPP__TRACING_IN_A_TRACE_PRODUCER"></span>トレースプロデューサーでの WPP トレースの有効化

-   TraceWPP (TraceWPP) は、カーネルモードドライバーやユーザーモードアプリケーションなど、[トレースプロバイダー](trace-provider.md)のソースファイルに対して Windows software trace プリプロセッサ (WPP) を実行するコマンドラインツールです。

    TraceWPP は、WDK と Visual Studio を使用してドライバーまたはアプリケーションをビルドするときに、WPP オプションを設定する代わりに使用できます。 このツールでは、ソースファイル内のトレースマクロを処理し、WPP トレースを有効にするヘッダーファイルを作成します。

    TraceWPP のコマンドラインオプションは、 [tracewpp タスク](tracewpp-task.md)が MSBuild に渡されるときに使用されるオプションと同じです。 これらのオプションの詳細については、「 [WPP プリプロセッサ](wpp-preprocessor.md)」を参照してください。

    TraceWPP は、WDK の bin\\&lt;*Platform*&gt; ディレクトリにあります。

### <a name="span-idcontrolling_trace_sessions__trace_controllers_spanspan-idcontrolling_trace_sessions__trace_controllers_spancontrolling-trace-sessions-trace-controllers"></a><span id="controlling_trace_sessions__trace_controllers_"></span><span id="CONTROLLING_TRACE_SESSIONS__TRACE_CONTROLLERS_"></span>トレースセッションの制御 (トレースコントローラー)

-   [Traceview](traceview.md) (traceview .exe) は、GUI ベースの[トレースコントローラー](trace-controller.md)と[トレースコンシューマー](trace-consumer.md)であり、特にトレースメッセージをリアルタイムで表示するために設計されています。 [トレースセッション](trace-session.md)の有効化、構成、開始、更新、停止を行います。 このツールでは、リアルタイムのトレースセッションと[トレースログ](trace-log.md)からトレースメッセージの形式を設定、フィルター処理、および表示することもできます。

    TraceView は、 [Traceview](tracepdb.md)、 [Traceview](tracelog.md)、および[tracefmt](tracefmt.md)の機能を組み合わせて拡張したものです。 詳細については、TraceView を開始し、[**ヘルプ**] メニューの [**ヘルプトピック**] をクリックします。

    TraceView は、WDK の tools\\&lt;*Platform*&gt; サブディレクトリにあります。ここで &lt;*Platform*&gt; は、x86 または x64 です。

-   [Tracelog](tracelog.md) (tracelog .exe) は、リアルタイムおよびログセッションを有効化、構成、開始、更新、および停止するコマンドライン[トレースコントローラー](trace-controller.md)です。 Tracelog では、ユーザーモードとカーネルモードのトレースセッションだけでなく、 [NT カーネルロガートレース](nt-kernel-logger-trace-session.md)セッションおよび[グローバル Logger (ブート) トレースセッション](global-logger-trace-session.md)もサポートされています。 このツールでは、遅延プロシージャ呼び出し (Dpc) と割り込みサービスルーチン (Isr) に費やされた時間を測定するトレースもサポートしています。

    Tracelog は、WDK の tools\\&lt;*Platform*&gt; サブディレクトリにあります。ここで &lt;*Platform*&gt; は、x86 または x64 です。

-   Logman (Logman) は、フル機能を備えた GUI ベースの[トレースコントローラー](trace-controller.md)であり、特にパフォーマンスカウンターおよびイベントトレースのログ記録を制御するように設計されています。

    Logman は、windows XP 以降のバージョンの Windows に含まれています。 このツールの使用方法の詳細については、「 [Logman](https://go.microsoft.com/fwlink/p/?linkid=179385)」を参照してください。

### <a name="span-idcreating_tmf_filesspanspan-idcreating_tmf_filesspancreating-tmf-files"></a><span id="creating_tmf_files"></span><span id="CREATING_TMF_FILES"></span>TMF ファイルを作成しています

-   [Tracepdb](tracepdb.md) (tracepdb) は、 [PDB シンボルファイル](pdb-symbol-files.md)のトレースメッセージ書式設定命令から[トレースメッセージ形式 (tmf) ファイル](trace-message-format-file.md)を作成するコマンドラインサポートツールです。

    トレースメッセージ、 [tracefmt](tracefmt.md)(tracefmt .exe)、 [traceview](traceview.md)(traceview .exe) を表示するツールでは、tmf ファイルの書式設定命令を使用して、トレースメッセージの書式設定と表示を行うことができます。

    また、tracefmt は、 [PDB シンボルファイル](pdb-symbol-files.md)から tmf ファイルを作成することもできます。

    Tracepdb と Tracefmt は、WDK の tools\\tracing\\&lt;*Platform*&gt; サブディレクトリにあります。 &lt;*Platform*&gt; は、x86 または x64 です。

### <a name="span-idformatting_and_displaying_trace_messages__trace_consumers_spanspan-idformatting_and_displaying_trace_messages__trace_consumers_spanformatting-and-displaying-trace-messages-trace-consumers"></a><span id="formatting_and_displaying_trace_messages__trace_consumers_"></span><span id="FORMATTING_AND_DISPLAYING_TRACE_MESSAGES__TRACE_CONSUMERS_"></span>トレースメッセージの書式設定と表示 (トレースコンシューマー)

-   [Tracefmt](tracefmt.md)は、*トレースメッセージ*(**TraceMessage**) をリアルタイムのトレースセッションまたはトレースログからフォーマットし、それらをファイルに書き込むか、コマンドプロンプトウィンドウに表示するコマンドライン[トレースコンシューマー](trace-consumer.md)です。

-   Tracerpt (Tracerpt) は、*トレースイベント*(**traceevent**) とパフォーマンスカウンターをフォーマットし、それらを CSV または XML ファイルに書き込むコマンドライン[トレースコンシューマー](trace-consumer.md)です。 また、イベントを分析し、概要レポートを生成します。

    Tracerpt は、windows XP 以降のバージョンの Windows に含まれています。 このツールの使用方法の詳細については、「 [Tracerpt](https://go.microsoft.com/fwlink/p/?linkid=179389)」を参照してください。

-   トレースコントローラーおよびトレースコンシューマーである[Traceview](traceview.md)は、トレースメッセージ (**TraceMessage**) を書式設定し、リアルタイムのトレースセッションまたはトレースログから表示します。 トレースメッセージは表形式で表示されるため、フィルター処理と参照が簡単になります。

### <a name="span-idviewing_trace_events_in_a_debuggerspanspan-idviewing_trace_events_in_a_debuggerspanviewing-trace-events-in-a-debugger"></a><span id="viewing_trace_events_in_a_debugger"></span><span id="VIEWING_TRACE_EVENTS_IN_A_DEBUGGER"></span>デバッガーでのトレースイベントの表示

-   Windows 用デバッグツールには、 **! wmitrace**が含まれています。これは、トレースセッションバッファーにトレースメッセージを表示する特殊なデバッガー拡張機能であり、ログファイルに書き込まれるか、表示するために配信されます。

-   [Tracelog](tracelog.md)および[tracelog](traceview.md)は、接続されているいずれかの方法で、トレースメッセージを KD または Windbg にリダイレクトできます。 詳細については、「Tracelog **-kd**パラメーター」と「Tracelog **Windbg**オプション」を参照してください。

### <a name="span-idanalyzing_dpc_and_isr_execution_timesspanspan-idanalyzing_dpc_and_isr_execution_timesspananalyzing-dpc-and-isr-execution-times"></a><span id="analyzing_dpc_and_isr_execution_times"></span><span id="ANALYZING_DPC_AND_ISR_EXECUTION_TIMES"></span>DPC と ISR の実行時間の分析

-   Windows XP Service Pack 2 (SP2) 以降では、 [Tracelog](tracelog.md)を使用して、NT カーネルロガートレースセッションで遅延プロシージャ呼び出し (DPC) イベントと割り込みサービスルーチン (ISR) イベントをログに記録してから、Tracerpt を使用してログから概要レポートを作成できます。 このツールの使用方法 (例を含む) の詳細については、「Tracelog」を参照してください。

 

 






---
title: TraceView の使用の準備
description: TraceView の使用の準備
ms.assetid: 724e3c8a-7760-4e53-8d44-1927e5ad1efd
keywords:
- TraceView WDK、使用の準備
- ファイル WDK トレースビュー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff2860f7a8705ef171ebdd702fbda0f08a4cd9ec
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769668"
---
# <a name="preparing-to-use-traceview"></a>TraceView の使用の準備


## <span id="ddk_preparing_to_use_traceview_tools"></span><span id="DDK_PREPARING_TO_USE_TRACEVIEW_TOOLS"></span>


TraceView を使用する前に、イベントトレースに関する情報と、トレースする[トレースプロバイダー](trace-provider.md)に関する情報を収集する必要があります。 このトピックでは、これらの前提条件について説明します。

**メモ**   Windows Vista より前のバージョンの Windows オペレーティングシステムで TraceView を実行している場合は、Dbghelp .dll ファイルを TraceView 実行可能ファイル (TraceView .exe) と同じサブディレクトリにコピーする必要があります。 

既定では、traceview .exe は \\ Windows Driver Kit (WDK) の tools* &lt; Platform &gt; *サブディレクトリにあります。ここで、 * &lt; &gt; Platform*は i386、amd64、または ia64 です。 Dbghelp .dll は、既定で \\ bin \\ x86 サブディレクトリにインストールされます。

 

### <a name="span-idunderstand_event_tracingspanspan-idunderstand_event_tracingspanunderstand-event-tracing"></a><span id="understand_event_tracing"></span><span id="UNDERSTAND_EVENT_TRACING"></span>イベントトレースについて

TraceView を使用する前に、*イベントトレース*について理解しておく必要があります。 詳細については、「 [WPP ソフトウェアのトレース](wpp-software-tracing.md)と[Windows イベントトレーシング](https://docs.microsoft.com/windows-hardware/test/wpt/event-tracing-for-windows)」を参照してください。

また、WPP ソフトウェアトレースでインストルメント化されたサンプルドライバーである Tracedrv (Tracedrv .c) を調べます。 [Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)サンプルは、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。 Tracedrv ドライバーとそのエンジン Tracectl (Tracectl) をビルドし、ドライバーとエンジンを使用して、TraceView を試します。

### <a name="span-idknow_the_trace_providerspanspan-idknow_the_trace_providerspanknow-the-trace-provider"></a><span id="know_the_trace_provider"></span><span id="KNOW_THE_TRACE_PROVIDER"></span>トレースプロバイダーについて

トレースする[トレースプロバイダー](trace-provider.md)と、トレースによって生成されるトレースメッセージの種類を理解している必要があります。

TraceView は、トレースイベントおよびトレースメッセージを人間が判読できる形式で表示しますが、それらを解釈したり、メッセージの情報やコンテキストを提供したりすることはありません。 メッセージとプロバイダーについての説明を理解するには、プロバイダーの操作に精通している必要があります。

### <a name="span-idfind_provider_filesspanspan-idfind_provider_filesspanfind-provider-files"></a><span id="find_provider_files"></span><span id="FIND_PROVIDER_FILES"></span>プロバイダーファイルの検索

トレースプロバイダーからのトレースメッセージを表示するには、次のいずれかの場所を TraceView に渡す必要があります。

-   プロバイダーの[PDB シンボルファイル](pdb-symbol-files.md)の場所

-   - または -

-   プロバイダーの[コントロール GUID (ctl) ファイル](control-guid-file.md)の場所と、トレースメッセージの[トレースメッセージ形式 (tmf) ファイル](trace-message-format-file.md)の場所です。

[NT カーネルロガーのトレースセッション](nt-kernel-logger-trace-session.md)では、WDK ( \\ tools \\ tracing \\ i386 に含まれている system. tmf ファイルを使用し \) ます。

これらのファイルと TraceView での使用方法については、「 [NT カーネルロガートレースセッションの作成](creating-an-nt-kernel-logger-trace-session.md)」で説明されています。 この情報は、トレースセッションを作成するときに使用します。

 

 






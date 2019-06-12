---
title: TraceView の使用の準備
description: TraceView の使用の準備
ms.assetid: 724e3c8a-7760-4e53-8d44-1927e5ad1efd
keywords:
- Traceview で WDK を使用する準備
- WDK traceview でのファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff91a47ea2c8a4a31b791d1d2acf870ccbdb1f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327333"
---
# <a name="preparing-to-use-traceview"></a>TraceView の使用の準備


## <span id="ddk_preparing_to_use_traceview_tools"></span><span id="DDK_PREPARING_TO_USE_TRACEVIEW_TOOLS"></span>


Traceview でを使用する前に約およびイベント トレース情報を収集する必要があります、[トレース プロバイダー](trace-provider.md)をトレースしています。 このトピックでは、これらの前提条件について説明します。

**注**   traceview で Windows オペレーティング システムを Windows Vista より前のバージョンを実行している場合は、TraceView.exe traceview で実行可能ファイルと同じサブディレクトリに Dbghelp.dll ファイルをコピーする必要があります。 

既定では、TraceView.exe はツールである\\ *&lt;プラットフォーム&gt;* サブディレクトリ Windows Driver Kit (WDK) の場所 *&lt;プラットフォーム&gt;* i386、amd64、または ia64 のいずれかです。 Dbghelp.dll がインストールされている、既定で、 \\bin\\x86 サブディレクトリ。

 

### <a name="span-idunderstandeventtracingspanspan-idunderstandeventtracingspanunderstand-event-tracing"></a><span id="understand_event_tracing"></span><span id="UNDERSTAND_EVENT_TRACING"></span>イベントのトレースを理解します。

理解しておく必要があります traceview でを使用する前に*イベント トレース*します。 詳細については、次を参照してください。 [WPP ソフトウェア トレース](wpp-software-tracing.md)と"[イベント トレーシング](https://go.microsoft.com/fwlink/p/?linkid=60384)"Microsoft Windows SDK のトピックです。

また、Tracedrv (Tracedrv.c)、WPP ソフトウェア トレースとインストルメント化されたドライバーのサンプルを確認します。 [Tracedrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)サンプルは、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507 )GitHub リポジトリにあります。 Tracedrv ドライバーとそのエンジン、Tracectl (Tracectl.c) をビルドし、traceview でみたりする場合、ドライバーとエンジンを使用します。

### <a name="span-idknowthetraceproviderspanspan-idknowthetraceproviderspanknow-the-trace-provider"></a><span id="know_the_trace_provider"></span><span id="KNOW_THE_TRACE_PROVIDER"></span>トレース プロバイダーを知る

理解しておく必要があります、[トレース プロバイダー](trace-provider.md)をトレースしていることと、トレースの種類のメッセージを生成します。

Traceview でトレースのイベントとトレース メッセージを人間が判読できる形式で表示されますが、それらを解釈したり、メッセージの情報やコンテキストを提供しません。 詳細については、メッセージとプロバイダーについて示すため、プロバイダーの操作をよく理解する必要があります。

### <a name="span-idfindproviderfilesspanspan-idfindproviderfilesspanfind-provider-files"></a><span id="find_provider_files"></span><span id="FIND_PROVIDER_FILES"></span>プロバイダーのファイルを検索します。

トレース プロバイダーからのトレース メッセージを表示するには、次の場所のいずれかを traceview でに提供する必要があります。

-   場所、 [PDB シンボル ファイル](pdb-symbol-files.md)プロバイダー

-   - または -

-   場所、[コントロール GUID (.ctl) ファイル](control-guid-file.md)プロバイダーとの位置の[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)そのトレース メッセージ

[NT Kernel Logger トレース Session](nt-kernel-logger-trace-session.md) WDK に含まれている system.tmf ファイルを使用して (\\ツール\\トレース\\i386\)します。

これらのファイル、およびその traceview での使用については説明[NT カーネル ロガーのトレース セッションを作成する](creating-an-nt-kernel-logger-trace-session.md)します。 この情報は、トレース セッションを作成するときに使用します。

 

 






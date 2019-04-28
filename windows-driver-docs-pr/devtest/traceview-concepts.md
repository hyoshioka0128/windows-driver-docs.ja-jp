---
title: TraceView の概念
description: TraceView の概念
ms.assetid: 4fab2b23-8f7b-407b-b944-41ac8caf1a75
keywords:
- Traceview で WDK、用語集
- WDK、グループのセッションをトレースします。
- トレース セッションをグループ化
- WDK traceview でワークスペースのワークスペースについて
- WDK、ワークスペースのセッションをトレースします。
- トレース プロバイダー WDK
- プロバイダーの WDK ソフトウェア トレース
- WDK、プロバイダーのセッションをトレースします。
- TMF ファイル WDK、検索パス
- 検索パスの WDK ソフトウェア トレース
- TMF ファイル WDK、オプション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4318021c115d9e983f4339eb94f50824fb28e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369625"
---
# <a name="traceview-concepts"></a>TraceView の概念

## <span id="ddk_traceview_concepts_tools"></span><span id="DDK_TRACEVIEW_CONCEPTS_TOOLS"></span>

このトピックでは、traceview で使用される概念を説明します。

WDK のトレース ツールに共通する概念については、次を参照してください。[トレース ツールの概念](tracing-tool-concepts.md)します。

### <a name="span-idtracesessiongroupspanspan-idtracesessiongroupspanspan-idtracesessiongroupspantrace-session-group"></a><span id="Trace_Session_Group"></span><span id="trace_session_group"></span><span id="TRACE_SESSION_GROUP"></span>トレース セッションのグループ

Traceview で結合できます。[トレース ログ](trace-log.md)表示またはリアルタイムのトレース セッションに、*トレース セッション グループ*し、1 つのセッションのように管理できます。 ときにトレース ログまたはセッションが同じトレース セッションのグループでは、そのメッセージは、1 つにまとめられています[トレース メッセージ一覧](trace-message-lists.md)します。

既定では、各トレース セッションは、そのトレース セッションのみで構成されるトレース セッションのグループのメンバーです。

トレース セッションのグループを作成する方法の詳細については、次を参照してください。[トレース セッションをグループ化](grouping-trace-sessions.md)します。

### <a name="span-idworkspacespanspan-idworkspacespanspan-idworkspacespanworkspace"></a><span id="Workspace"></span><span id="workspace"></span><span id="WORKSPACE"></span>ワークスペース

Traceview で、*ワークスペース*一連のトレース セッションのプロパティとトレース ログは、表示プロパティを保存して再利用することができます。 ワークスペースでは、頻繁に使用されるログを表示したり、1 つの簡単な手順で慎重に構成済みのトレース セッションを開始できます。

ワークスペースは次のとおりです。

- バッファー、フラグとレベル、およびトレース ログの場所を含め、トレース セッションのすべてのプロパティ

- 場所、[プログラム データベース (PDB) シンボル ファイル](pdb-symbol-files.md)、[トレース メッセージの形式 (TMF) ファイル](trace-message-format-file.md)、または TMF 検索パス

- Traceview でのファイルおよび概要ファイルの一覧のパスとファイル名

- [フィルター](filtering-trace-messages.md)

リアルタイムのトレース セッションのワークスペースを開くと、traceview では、保存されているプロパティおよび構成設定の新しいトレース セッションを開始します。 トレース ログの表示のためのワークスペースを開くと、それを構成したとおり、ログが表示されます。

詳細については、次を参照してください。 [traceview でワークスペースを使用して](using-traceview-workspaces.md)します。

### <a name="span-idspecifyingtraceprovidersspanspan-idspecifyingtraceprovidersspanspan-idspecifyingtraceprovidersspanspecifying-trace-providers"></a><span id="Specifying_Trace_Providers"></span><span id="specifying_trace_providers"></span><span id="SPECIFYING_TRACE_PROVIDERS"></span>トレース プロバイダーを指定します。

トレース セッションを作成するにはトレース プロバイダーを識別して、プロバイダーが生成されるバイナリのトレース メッセージの書式設定命令を検索します。 このいずれかの方法は、次を行うことができます。

- プロバイダーの行をソース コードの実行可能バイナリを検索します。 Traceview で有効にして、書式設定に必要なすべての情報を抽出できます[TraceLogging](https://msdn.microsoft.com/library/windows/desktop/dn904636)と ETW イベントを指します。 検索を試みます、 [PDB シンボル ファイル](pdb-symbol-files.md)を有効にする[WPP ソフトウェア トレース](wpp-software-tracing.md)プロバイダー。

- 検索、 [PDB シンボル ファイル](pdb-symbol-files.md)を含むソース コードの[WPP ソフトウェア トレース](wpp-software-tracing.md)プロバイダー。 Traceview では、pdb ファイルから抽出できるファイルのすべてのプロバイダーを識別し、トレース メッセージの書式を設定する必要がある情報。

- 検索、[コントロール GUID (.ctl) ファイル](control-guid-file.md)プロバイダーの指定、 [TMF ファイル](trace-message-format-file.md)または TMF ファイルが格納されるディレクトリへのパス。

- 入力、[コントロール GUID](control-guid.md)プロバイダーの TMF ファイルまたは TMF ファイルが格納されるディレクトリへのパスを指定します。

    アスタリスクの前にプロバイダー名を入力するかどうか (例: ```*SampleProvider```)、traceview では標準アルゴリズムを使用して GUID に名前を自動的に起動します。 一部のプロバイダーにプロバイダーを使用して記述など、多くが、この標準に従う[します。NET の EventSource](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.tracing.eventsource)、操作を行います。

- 選択、[登録済みのプロバイダー](registered-provider.md)一覧からその traceview でアセンブルし、TMF ファイルまたは TMF ファイルが格納されるディレクトリのパスを指定します。

- 選択、 [NT Kernel Logger トレース Session](nt-kernel-logger-trace-session.md)トレースに 1 つまたは複数のオペレーティング システムのイベントを選択します。

### <a name="span-idsettmfsearchpathandselecttmffilesoptionsspanspan-idsettmfsearchpathandselecttmffilesoptionsspanspan-idsettmfsearchpathandselecttmffilesoptionsspanset-tmf-search-path-and-select-tmf-files-options"></a><span id="Set_TMF_Search_Path_and_Select_TMF_Files_Options"></span><span id="set_tmf_search_path_and_select_tmf_files_options"></span><span id="SET_TMF_SEARCH_PATH_AND_SELECT_TMF_FILES_OPTIONS"></span>TMF 検索パスと選択 TMF ファイル オプションを設定します。

ない限り、WPP プロバイダーを有効にする場合、 [PDB シンボル ファイル](pdb-symbol-files.md)provider では、traceview でが TMF ファイルを検索できるまたは見つける必要がありますディレクトリを指定する必要があります、 [TMF ファイル](trace-message-format-file.md)プロバイダーのトレース メッセージ。

Traceview では、2 つのメソッドをサポートしています。

- 使用して、 **TMF 検索パスの設定**かわからない TMF がファイル トレース プロバイダーを使用するときのオプションします。 Traceview では、指定されたディレクトリに TMF ファイルのすべてを検索し、メッセージ TMF ファイルの名前に生成されるメッセージの GUID と一致します。 TMF ファイルは、指定したディレクトリ内になければなりません。 Traceview では、再帰的には検索されません。

- 使用して、**選択 TMF ファイル**TMF は、トレース プロバイダーを使用するファイルまたは別のディレクトリにする必要がある TMF ファイルがわかっている場合のオプションします。 TMF ファイルの名前がない場合にも、このオプションを使用する必要があります、[メッセージ GUID](message-guid.md)が traceview でを使用すると、ディレクトリで見つけることはできません。

指定されている TMF ファイルや、traceview では、指定されたディレクトリで検索するにはトレース プロバイダーによって生成されるトレース メッセージと一致しない場合、traceview では、メッセージをフォーマットできません。 代わりに、トレース メッセージの GUID と、次のエラー メッセージが表示されます。

```
No Format Information found.
```

コマンド プロンプト ウィンドウで、PDB シンボル ファイルから TMF ファイルを作成するには使用[Tracepdb](tracepdb.md)します。

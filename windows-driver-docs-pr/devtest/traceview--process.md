---
title: TraceView -process
description: Traceview でを使用して、トレース ログまたはトレースのリアルタイム seesion からのバイナリ トレース メッセージを書式設定するコマンドを処理します。 Traceview で-プロセス コマンドは、トレース メッセージのテキスト ファイルおよび入力と出力ファイルを説明する概要ファイルを作成します。
ms.assetid: a0da5004-7a9f-4229-92c1-6264fcbf9b0d
keywords:
- Traceview でのドライバーの開発ツールの処理
topic_type:
- apiref
api_name:
- TraceView -process
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57d39635eb39d4dbe05ac74f01e1cbd127e439ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369613"
---
# <a name="traceview--process"></a>TraceView -process


使用して、 **traceview で-プロセス**バイナリのトレースを書式設定コマンドのメッセージを[トレース ログ](trace-log.md)またはリアルタイム トレース seesion から。 **Traceview で-プロセス**トレース メッセージのテキスト ファイルと、入力と出力ファイルを説明する概要ファイルが作成されます。

```
    traceview -process [EtlFile | -rt SessionName][Parameters]
   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター

<span id="_______EtlFile______"></span><span id="_______etlfile______"></span><span id="_______ETLFILE______"></span> *EtlFile*   
トレース メッセージを含むイベント トレース ログ (.etl) ファイルを指定します。 (省略可能) のパスとファイル名を入力します。 既定値は c:\\logfile.etl します。

<span id="_______-rt_______SessionName______"></span><span id="_______-rt_______sessionname______"></span><span id="_______-RT_______SESSIONNAME______"></span> **-rt** *SessionName*   
リアルタイムです。 形式は、指定されたリアルタイム トレース セッションからのメッセージをトレースします。

*SessionName*トレース セッションの名前を指定します。 Tracefmt 形式からのメッセージでトレース セッション名を省略した場合、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

<span id="_______-tmf_______TMFFile______"></span><span id="_______-tmf_______tmffile______"></span><span id="_______-TMF_______TMFFILE______"></span> **-tmf** *TMFFile*   
ファイル名とパス (省略可能) を指定します、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース メッセージ。

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span> **-p** *TMFPath*   
含むディレクトリへのパスを指定します、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース メッセージ。

<span id="_______-o_______OutputFile______"></span><span id="_______-o_______outputfile______"></span><span id="_______-O_______OUTPUTFILE______"></span> **-o** *OutputFile*   
出力ファイルの名前を指定します。 この名前は、書式設定済みトレース メッセージのテキスト ファイルと概要ファイルに適用されます。

*OutputFile* .txt ファイル名拡張子、c: などのパスとファイル名は、\\トレース\\trace.txt します。 既定値は、FmfFile.txt FmtSum.txt ローカル ディレクトリにします。

このパラメーターを使用する場合、 **- と**または **- summaryonly**パラメーター、概要ファイルのみに影響を与えます。

<span id="_______-csv______"></span><span id="_______-CSV______"></span> **-csv**   
トレース ログをコンマで区切られた、変数の値 (.csv) ファイルとして書式設定します。

<span id="_______-display______"></span><span id="_______-DISPLAY______"></span> **-display**   
出力ファイルに書き込むだけでなく、コマンド プロンプト ウィンドウで、トレース メッセージを表示します。

<span id="_______-displayonly______"></span><span id="_______-DISPLAYONLY______"></span> **-と**   
コマンド プロンプト ウィンドウでのみ、トレース メッセージを表示します。 Traceview では、トレース メッセージのテキスト ファイルを作成できません。

<span id="_______-nosummary______"></span><span id="_______-NOSUMMARY______"></span> **-nosummary**   
作成されません、[概要メッセージ ファイル](summary-message-file.md)します。

<span id="_______-summaryonly______"></span><span id="_______-SUMMARYONLY______"></span> **-summaryonly**   
のみを作成、[概要メッセージ ファイル](summary-message-file.md)します。 Tracefmt は作成されません、[出力ファイル](tracefmt-output-file.md)します。

<span id="_______-noprefix______"></span><span id="_______-NOPREFIX______"></span> **-noprefix**   
省略、[トレース メッセージのプレフィックス](trace-message-prefix.md)します。 このパラメーターは、出力ファイルおよび Tracefmt 表示のトレース メッセージに影響します。

<span id="_______-ods______"></span><span id="_______-ODS______"></span> **-ods**   
表示のデバッガーを書式設定済みトレース メッセージを送信します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細。 Tracefmt は、各ブロックまたはトレース メッセージのバッファーを処理するときは、詳細、コマンド プロンプト ウィンドウで情報を表示します。 ファイルの破損または不整合が疑われる場合は、このパラメーターを使用します。

<span id="_______-h_____"></span><span id="_______-H_____"></span> **-h** | **/?**  
ヘルプを表示します。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

```
traceview -process
traceview -process mytrace.etl -p c:\tracing -o mytrace.txt
traceview mytrace.etl -tmf c:\tracing\37753236-c81f-505e-d40a-128d3bb2b5ff.tmf
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt -display
```

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

トレース メッセージの書式を設定するには、トレース メッセージのトレース メッセージのフォーマット ファイルを指定する必要があります。 使用可能なメソッドは、優先順位の順序のとおりです。

-   **- Tmf**パラメーター。

-   **-P**パラメーター。

-   トレース %\_形式\_検索\_%path% 環境変数。 TMF ファイルが配置されているディレクトリに、変数の値を設定します。

TMF のファイル名がない場合、 [GUID をメッセージ](message-guid.md)を使用して、 **- tmf**パラメーター ファイルへの完全修飾パスを入力します。 それ以外の場合、traceview でには、TMF ファイルが見つかりません。

Traceview では、TMF ファイルを見つけることができません、または TMF ファイルでは、トレース メッセージの書式設定情報は含まれません、traceview では、メッセージを書式設定できません。 代わりに、メッセージのテキストの代わりに traceview でを書き込みます。「なしの形式情報が見つかりません。」

Traceview では、トレース メッセージに書式を設定できない場合、例外が発生し、ようメッセージが表示されます。

```
*****FormatMessage Header(Header) of EventTrace, parameter 23 raised an exception*****
```

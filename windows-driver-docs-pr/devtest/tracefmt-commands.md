---
title: Tracefmt のコマンド
description: Tracefmt を使用するには、コマンド プロンプト ウィンドウで、コマンドを入力します。
ms.assetid: 79e56383-ce67-4716-98d6-4266b76a4b0a
keywords:
- Tracefmt は、ドライバー開発ツールをコマンドします。
topic_type:
- apiref
api_name:
- Tracefmt Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d0adf7bf6bef32e451d84b0c05fb13aa9f2c59f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578203"
---
# <a name="tracefmt-commands"></a>Tracefmt のコマンド


Tracefmt を使用するには、コマンド プロンプト ウィンドウで、コマンドを入力します。 次の構文には、Tracefmt コマンドの要素が表示されます。

トレース メッセージを読みやすい形式で表示するには、Tracefmt は、トレース メッセージをトレース メッセージのフォーマット ファイルで書式設定の手順を適用する必要があります。 使用する構文は、トレース プロバイダーの TMF ファイルがあるかどうか、または Tracefmt TMF ファイルを作成するかどうかによって異なります。

TMF ファイルまたは TMF ファイルのディレクトリへのパスを指定します。

```
    tracefmt [EtlFile | -rt SessionName][-tmf TMFFile | -p TMFPath ] [Options]
```

TMF ファイルを作成します。

```
    tracefmt [EtlFile | -rt SessionName]-i ImageFiles [-r SymbolPath ] [-p TmfPath ] [Options]
```

コマンドライン構文を表示します。

```
    tracefmt -h | /?
```

## <a name="span-idddktracefmtcommandstoolsspanspan-idddktracefmtcommandstoolsspanparameters"></a><span id="ddk_tracefmt_commands_tools"></span><span id="DDK_TRACEFMT_COMMANDS_TOOLS"></span>パラメーター


<span id="_______EtlFile______"></span><span id="_______etlfile______"></span><span id="_______ETLFILE______"></span> *EtlFile*   
トレース メッセージを含むイベント トレース ログ (.etl) ファイルを指定します。 (省略可能) のパスとファイル名を入力します。 既定値は c:\\logfile.etl します。

<span id="_______-rt________SessionName______"></span><span id="_______-rt________sessionname______"></span><span id="_______-RT________SESSIONNAME______"></span> **-rt** *SessionName*   
リアルタイムです。 代わりに、指定されたリアルタイム トレース セッションからのメッセージをトレース形式、[トレース ログ](trace-log.md)します。

*SessionName*トレース セッションの名前を指定します。 既定値は[NT Kernel Logger](nt-kernel-logger-trace-session.md)します。

<span id="_______-tmf_______TMFFile______"></span><span id="_______-tmf_______tmffile______"></span><span id="_______-TMF_______TMFFILE______"></span> **-tmf** *TMFFile*   
ファイル名とパス (省略可能) を指定します、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)トレース メッセージ。 既定値は、Default.tmf、WDK に含まれるファイルです。

<span id="_______-i_______ImageFiles______"></span><span id="_______-i_______imagefiles______"></span><span id="_______-I_______IMAGEFILES______"></span> **-i** *ImageFiles*   
指定したイメージ ファイルの PDB シンボル ファイルを検索し、PDB ファイルで書式設定の手順から TMF ファイルを作成する Tracefmt に指示します。

*画像ファイル*の (.exe、.dll、または .sys) 1 つまたは複数のバイナリ ファイルのパスとファイルの名前を表す[トレース プロバイダー](trace-provider.md)します。 セミコロン (;) の使用します。イメージ ファイルの名前を区切ります。

<span id="_______-r_______SymbolPaths______"></span><span id="_______-r_______symbolpaths______"></span><span id="_______-R_______SYMBOLPATHS______"></span> **-r** *SymbolPaths*   
プライベートの PDB シンボル ファイルの場所を指定してで指定されたイメージ ファイルの **-i**します。

*SymbolPaths*プライベート シンボルを格納またはサーバー パスをシンボル ディレクトリへの 1 つまたは複数のパスを表します。 セミコロン (;) の使用します。パス名を区切ります。 内のパス名*SymbolPaths*アスタリスクなどのワイルドカード文字を含めることができます (\*) 複数の文字と 1 つの文字を表す疑問符 (?) を表します。

含める場合 **-i**コマンドでは省略 **-r**、Tracepdb % で指定されたパス内の指定したイメージの PDB ファイルを検索\_NT\_シンボル\_%Path% 環境変数。 環境変数が設定されていない場合 Tracepdb が、既定のシンボル パスで検索**srv\*\\\\\\\\シンボル\\\\シンボル**.

<span id="_______-p_______TMFPath______"></span><span id="_______-p_______tmfpath______"></span><span id="_______-P_______TMFPATH______"></span> **-p** *TMFPath*   
TMF ファイルを格納するディレクトリへのパスを指定します。

ときに **-p**せずに使用されます **-i**、によって指定されたパスの中から検索 Tracefmt **-p**既存の TMF ファイルします。 場合 **-p** TMF ファイル トレース % の値を省略した場合の Tracefmt が検索\_形式\_検索\_%path% 環境変数、設定されている場合。 それ以外の場合、Tracefmt は Default.tmf ファイルで書式設定の手順を適用しようとします。

ときに **-p**併用 **-i**、Tracefmt 配置 TMF ファイルで指定されたディレクトリで作成した **-p**します。 場合 **-p**は省略すると、Tracefmt TMF ファイル ディレクトリに配置トレース % の値で指定された\_形式\_検索\_%path% 環境変数、設定されている場合。 それ以外の場合、Tracefmt は、ローカル ディレクトリにファイルを配置します。

<span id="_______-h_____"></span><span id="_______-H_____"></span> **-h** | **/?**  
ヘルプを表示します。

<span id="_______-o_______OutputFile______"></span><span id="_______-o_______outputfile______"></span><span id="_______-O_______OUTPUTFILE______"></span> **-o** *OutputFile*   
代替名を指定します、 [Tracefmt 出力ファイル](tracefmt-output-file.md)と[Tracefmt 概要メッセージ ファイル](summary-message-file.md)します。 既定値は、(出力ファイル) の FmfFile.txt と FmtSum.txt.sum (概要ファイル) をローカル ディレクトリには。

*OutputFile* .txt ファイル名拡張子、c: などのパスとファイル名は、\\トレース\\trace.txt します。

このパラメーターを使用する場合、 **- と**または **- summaryonly**オプション、概要メッセージ ファイルのみに影響を与えます。

<span id="_______-csv______"></span><span id="_______-CSV______"></span> **-csv**   
書式設定、 [Tracefmt 出力ファイル](tracefmt-output-file.md)をコンマで区切られた、変数の値 (.csv) ファイルとして。 この形式を構造化された詳細なプレフィックスを追加します、各メッセージをさらに、標準[トレース メッセージのプレフィックス](trace-message-prefix.md)します。

このオプションは、出力ファイルを存在する場合に、コマンド プロンプト ウィンドウで、トレース メッセージの表示を与えます。

<span id="_______-csvheader______"></span><span id="_______-CSVHEADER______"></span> **-csvheader**   
CSV ファイルには、わかりやすい列の見出しの行を追加します。 このヘッダーは Tracefmt を CSV ファイルに追加する構造化されたプレフィックスを解釈するために特に便利です。 既定では、Tracefmt CSV ファイルに列見出しはありません。

<span id="_______-csvquote______"></span><span id="_______-CSVQUOTE______"></span> **-csvquote**   
すべて引用符 (") で、CSV ファイルに 2 倍になります。 この機能は、引用符を引用符で囲まない場合にのみ表示するアプリケーションに適しています。

<span id="_______-display______"></span><span id="_______-DISPLAY______"></span> **-display**   
出力ファイルに書き込むだけでなく、コマンド プロンプト ウィンドウで、トレース メッセージを表示します。

<span id="_______-displayonly______"></span><span id="_______-DISPLAYONLY______"></span> **-と**   
コマンド プロンプト ウィンドウでのみトレース メッセージを表示し、出力ファイルを作成できません。

<span id="_______-nosummary______"></span><span id="_______-NOSUMMARY______"></span> **-nosummary**   
作成されません、[概要メッセージ ファイル](summary-message-file.md)します。

<span id="_______-summaryonly______"></span><span id="_______-SUMMARYONLY______"></span> **-summaryonly**   
のみを作成、[概要メッセージ ファイル](summary-message-file.md)します。 Tracefmt は作成されません、[出力ファイル](tracefmt-output-file.md)します。

<span id="_______-noprefix______"></span><span id="_______-NOPREFIX______"></span> **-noprefix**   
省略、[トレース メッセージのプレフィックス](trace-message-prefix.md)します。 このオプションでは、出力ファイルおよび Tracefmt 表示のトレース メッセージに影響します。

<span id="_______-hires______"></span><span id="_______-HIRES______"></span> **-人材採用**   
高解像度。 トレース メッセージのタイムスタンプでは、マイクロ秒およびナノ秒数を表示します。 既定ではミリ秒のみが表示されます。

トレース メッセージ タイム スタンプ場合など、システム タイマーではなく、パフォーマンス カウンターのクロック値が使用される場合は、このオプションを使用、 **Tracelog UsePerfCounter**パラメーターを使用します。 Tracelog コマンドについては、次を参照してください。 [ **Tracelog コマンド構文**](tracelog-command-syntax.md)します。

<span id="_______-seq______"></span><span id="_______-SEQ______"></span> **-seq**   
内のローカルまたはグローバルのシーケンス番号が表示されます、[トレース メッセージのプレフィックス](trace-message-prefix.md)します。 シーケンス番号がメッセージに記録されていない場合、フィールドが初期化されていない、または、ゼロまたは"f"の s で塗りつぶすこと。

<span id="_______-ods______"></span><span id="_______-ODS______"></span> **-ods**   
表示のデバッガーを書式設定済みトレース メッセージを送信します。

<span id="_______-gmt______"></span><span id="_______-GMT______"></span> **-gmt**   
グリニッジ標準時 (GMT) での各トレース メッセージのタイムスタンプが表示されます。

このオプションでは、Tracefmt の出力ファイルだけに影響します。 時刻のスタンプは、イベント トレース ログ (.etl) ファイルは変換されません。 Tracefmt コマンドを送信するときに、トレース ログのタイム ゾーンが表示されます。

<span id="_______-utc______"></span><span id="_______-UTC______"></span> **-utc**   
各トレース メッセージで世界協定時刻 (UTC) タイムスタンプが表示されます。 UTC は、GMT とほぼ同じですが、0 として午前 0 時を表します。

このオプションでは、Tracefmt の出力ファイルだけに影響します。 時刻のスタンプは、イベント トレース ログ (.etl) ファイルは変換されません。 Tracefmt コマンドを送信するときに、トレース ログ ファイルのタイム ゾーンが表示されます。

<span id="_______-trace______"></span><span id="_______-TRACE______"></span> **-trace**   
発生すると、Tracefmt アクションが表示されます。 この情報は、ときに書式設定、正しくないまたは Tracefmt がエラーまたは例外を報告する場合に便利です。

広範なトレースの表示ができます。 Tracefmt 出力を後で調べるのためにテキスト ファイルにリダイレクトすることを検討してください。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細。 Tracefmt は、各ブロックまたはトレース メッセージのバッファーを処理するときは、詳細、コマンド プロンプト ウィンドウで情報を表示します。 ファイルの破損または不整合疑いがある場合は、このオプションを使用します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**TMF ファイルの検索**

省略した場合、 **-i** TMF ファイルを検索するパラメーター、Tracefmt の使用、次の方法です。 メソッドは、Tracefmt を使用する順序で一覧表示されます。

-   **- Tmf**パラメーター。

-   **-P**パラメーター。

-   トレース %\_形式\_検索\_%path% 環境変数。

-   Default.tmf、WDK に含まれるファイル。

Tracefmt TMF ファイルを見つけることができません、または TMF ファイルでは、トレース メッセージの書式設定情報は含まれません、Tracefmt は、メッセージを表示できません。 代わりに、トレース メッセージの代わりに、次のエラー メッセージを書き込みます

```
No Format Information found.
```

**例外が発生しました**

Tracefmt はトレース メッセージのパラメーターに書式を設定できない場合、例外が発生し、ようメッセージが表示されます。

```
*****FormatMessage Header(Header) of EventTrace, parameter 23 raised an exception*****
```

同様の例外を発生する場合は、任意のユーザーが指定した変数型に特に注意して、ソース コードのメッセージ定義を確認します。 詳細については、次を参照してください。 [ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)します。

**非 GUID ファイル名を持つ TMF ファイル**

TMF のファイル名がない場合、[メッセージ GUID](message-guid.md)ファイルを識別し、ファイルへの完全修飾パスを入力します。-tmf パラメーターを使用する必要があります。

**NT Kernel Logger トレース メッセージの書式設定**

メッセージの形式を[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)または[グローバル ロガー トレース セッション](global-logger-trace-session.md)、system.tmf ファイルを指定する - tmf パラメーターを使用して、[トレース メッセージのフォーマット ファイル](trace-message-format-file.md) WDK に含まれる.

**リアルタイムのトレース セッションからのトレース メッセージを書式設定**

使用すると、 **-rt** Tracefmt の (リアルタイム) のパラメーターは、リアルタイムのモードでし、指定されたトレース プロバイダーからのトレース メッセージを待機を確認するメッセージが表示されます。 トレース セッションを停止するまでは、コマンド プロンプトに戻ることはありません。

**QPC の時刻スタンプを書式設定**

Tracefmt がシステム パフォーマンス カウンターのクロックの値を書式設定しません (**QueryPerformanceCounter**) 正しくします。 この高解像度の時間を使用している場合は、Tracerpt、Windows XP および Windows での以降のバージョンに含まれるツールを使用して、トレース メッセージを書式設定。 詳細については、の説明を参照して、 **- UsePerfCounter**パラメーター [ **Tracelog コマンド構文**](tracelog-command-syntax.md)します。

**シーケンスのトレース メッセージ**

Windows XP を実行しているコンピューター上のトレース メッセージ ファイルを表示するシーケンス外のトレース メッセージが表示可能性があります。 この問題を解決するには、トレース セッションを開始および Tracefmt を使用してトレースを表示するときに、シーケンス番号オプションを使用できます。 Traceview でと並べ替え順序番号に従ってトレースを表示できます。 Windows Server 2003 または以降のバージョンの Windows を実行するコンピューターでトレースを表示することもできます。










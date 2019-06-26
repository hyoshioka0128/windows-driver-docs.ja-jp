---
title: Te.exe のコマンド オプション
description: Te.exe のコマンド オプション
ms.assetid: E9A9292D-FA30-410d-9322-BD0F321314F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d71cb48a3e99edfaba7a03abc0704f544d3d5ff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372986"
---
# <a name="teexe-command-options"></a>Te.exe のコマンド オプション

## <a name="usage"></a>使用方法

**te.exe** \<[テスト\_バイナリ](#test_binaries)> \[[/appendWttLogging](#appendwttlogging) \] \[ [/breakOnCreate](#breakoncreate) \] \[ [/breakOnError](#breakonerror) \] \[ [/breakOnInvoke](#breakoninvoke) \] \[ [/coloredConsoleOutput](#coloredconsoleoutputtruefalse) \] \[ [/console:flushWrites](#consoleflushwrites) \] \[ [/console:positionを=\[x, y |現在\]](#consolepositionxy--current-) \[ [/console:size =&lt;x, y&gt; \] ](#consolesize-xy--current-) \[ [/console: 最上位\] ](#consoletopmost) [ \[/defaultAppDomain\] ](#defaultappdomain) \[ [/disableConsoleLogging](#disableconsolelogging) \] \[ [/disableTimeouts](#disabletimeouts) \] \[ [/dpiaware](#dpiaware) \] \[ [/enableWttLogging](#enablewttlogging) \] \[ [/inproc](#inproc) \] \[ [/isolationLevel](#isolationlevellevel) \]\[ [/labMode](#labmode) \] \[ [/list](#list) \] \[ [/list プロパティ](#listproperties)\] \[ [/logFile:&lt;名前&gt;](#logfilename) \] \[ [/logOutput:&lt;モード&gt;](#logoutputmode) \] \[ [/miniDumpOnCrash](#minidumponcrash) \] \[ [/miniDumpOnError](#minidumponerror) \] \[ [/name:&lt;testname&gt; ](#nametestname) \] \[[/outputFolder:&lt;folderName&gt; ](#outputfolderfoldername) \] \[ [/p:&lt;ParamName&gt;=<span class="notra class=""></span class="notra>&gt;](#wttdevicestringsuffixvalue)\]

## <a name="selectionexecution-commands"></a>選択/実行コマンド

### <a name="testbinaries"></a>test_binaries

(スペースで区切られた) を実行する 1 つまたは複数のテスト ファイルを指定します。 ワイルドカード文字がサポートされています。

#### <a name="teexe-test1dll"></a>te.exe test1.dll

**解釈します。** Test1.dll ですべてのテストを実行します。

#### <a name="teexe-test1dll-test2dll-test3dll"></a>te.exe test1.dll test2.dll test3.dll

**解釈します。** Test1.dll、test2.dll test3.dll ですべてのテストを実行します。

#### <a name="teexe-dll"></a>te.exe \*.dll

**解釈します。** 現在のディレクトリ内のすべての dll では、すべてのテストを実行します。

### <a name="coloredconsoleoutputtruefalse"></a>/coloredConsoleOutput:\<true/false>

TAEF が色付きのコンソールのテキストを出力するかどうかを指定します。 既定値は true です。 False に設定する TAEF はコンソールの既定の色ですべてのテキストを出力します。

`te.exe test1.dll /coloredConsoleOutput:false`

### <a name="consoleoptionnamevalue"></a>/console:\<optionName>=\<value>

コンソールの TE の使用を構成するためのオプションを提供します。 次のオプションが使用できます。

#### <a name="consoleflushwrites"></a>/console:flushWrites

により、コンソール出力は、フラッシュ TE.exe の出力がリダイレクトされたときにすべての行が書き込まれた - に有効です。

#### <a name="consolepositionxy--current-"></a>/console:position=\[x,y | current \]

プライマリ モニター上隅に対して相対的にコンソール ウィンドウの位置をピクセル単位で設定します。 値を使用して、**現在**コンソールの現在の位置を格納されているし、再起動から再開するときに使用することを指定します。

#### <a name="consolesize-ltxygt--current-"></a>/console:size=\[ &lt;x,y&gt; | current \]

(文字ディメンション) で、コンソール ウィンドウのサイズを設定します。 画面バッファーのサイズは、必要に応じて、ウィンドウのサイズに合わせて増加はします。 値を使用して、**現在**を現在のコンソールのサイズを格納されているし、再起動から再開するときに使用することを指定します。

#### <a name="consoletopmost"></a>/console:topmost

実行中のデスクトップの z オーダーで ' 最上位' te.exe を実行しているコンソールを保持します。

### <a name="dpiaware"></a>/dpiaware

プロセスでテストを実行します。 DPI 対応としてマークされると、を参照してください[高 DPI](https://docs.microsoft.com/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)します。 これは、メタデータ ("DpiAware") を使用して設定できます。

### <a name="inproc"></a>/inproc

TE 内ではなく、TE.exe プロセス自体内のすべてのテストを実行します。ProcessHost.exe します。

te.exe test1.dll /inproc

> [!NOTE]
> TE が一度に 1 つのテスト dll の実行をサポートしてのみを使用する場合、 */inproc*設定します。

### <a name="isolationlevellevel"></a>/isolationLevel:\<レベル >

最小 TAEF テストを実行するときに使用する分離レベルを指定します。 この値は、メタデータとして指定された IsolationLevel と競合している場合は、最も厳しいスコープの分離レベルが値になります。 参照してください[テストの分離](test-isolation.md)の詳細。

`te.exe test1.dll /isolationLevel:Class`

### <a name="labmode"></a>/labMode

テストを実行し、潜在的なブロッキング UI (たとえば、Windows エラー報告ダイアログ ボックスでテストをクラッシュ) を削除します。

### <a name="list"></a>/list

すべての名前を一覧表示、[テスト\_バイナリ](#test_binaries)クラスとそれらに含まれるメソッド。 選択条件が指定されている場合は、条件を満たしているものの名前のみを一覧表示します。

```cpp
 te.exe test1.dll test2.dll /list

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example1
  WEX::UnitTests::Test1::Example2
  WEX::UnitTests::Test1::Example3

 WEX::UnitTests::Test2
  WEX::UnitTests::Test2::Example1
  WEX::UnitTests::Test2::Example2
  WEX::UnitTests::Test2::Example3
```

```cpp
 te.exe test1.dll test2.dll /select:@name='*Example2*' /list

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example2

 WEX: :UnitTests::Test2
  WEX::UnitTests::Test2::Example2
```

### <a name="listproperties"></a>/listProperties

名前と、すべてのテストのプロパティを一覧表示\_場合は、使用可能な関数名のバイナリと、クラスとセットアップと破棄と共にそれらのメソッド。 選択条件が指定されている場合は、条件を満たしているものの名前のみを一覧表示します。

```cpp
 te.exe test1.dll test2.dll /listProperties

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example1
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = MTA
  WEX::UnitTests::Test1::Example2
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = STA
  WEX::UnitTests::Test1::Example3
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = STA

 WEX::UnitTests::Test2
  WEX::UnitTests::Test2::Example1
   Property[ThreadingModel] = MTA
  WEX::UnitTests::Test2::Example2
   Property[ThreadingModel] = STA
  WEX::UnitTests::Test2::Example3
   Property[ThreadingModel] = MTA
```

```cpp
 te.exe test1.dll test2.dll /select:@name='*Example2*' /listProperties

 WEX::UnitTests::Test1
  WEX::UnitTests::Test1::Example2
   Setup: Test1Setup
   Teardown: Test1Teardown
   Property[ThreadingModel] = STA

 WEX::UnitTests::Test2
  WEX::UnitTests::Test2::Example2
   Property[ThreadingModel] = STA
```

### <a name="nametestname"></a>/name:\<testname>

テストのベース名の選択に代わる簡単なは"/select:@Name='&lt;testname&gt;'"です。 &lt;Testname&gt;ワイルドカード文字を含めることができますが ("\*「と」?")、単一引用符で囲んでいないに含まれる必要がありますが、します。 リンクと/name 両方がコマンド プロンプトで指定し、/選択場合は、クエリが優先され、/name は無視されます。

te.exe test1.dll /name:\*TestToLower  

**解釈します。** メソッド名がどこで 'TestToLower' で終了 test1.dll ですべてのテストを実行します。 選択条件として使用して同じ表現できる/select:@Name='\*TestToLower'。

te.exe test1.dll /name:\*StringTest\*  

**解釈します。** その名前空間、クラスまたはメソッド名に 'StringTest' test1.dll という語句を含むすべてのテストを実行します。

### <a name="outputfolderfoldername"></a>/outputFolder:\<folderName>

生成されたすべてのファイルを配置するフォルダーを指定します。 既定値は現在のディレクトリです。 たとえば、環境変数を使用できます。

`te.exe test1.dll /outputFolder:%TEMP%\\MyOutput`

### <a name="pparamnameparamvalue"></a>/p:\<ParamName>=\<ParamValue>

パラメーターの名前を持つランタイム パラメーターを定義します。 ParamName とパラメーターの値を = ParamValue を = です。 これらのパラメーターは、テスト メソッドまたはセットアップ/クリーンアップのメソッドからアクセスできます。

`te.exe test1.dll /p:x=5 /p:myParm=cool`

取得することができます、テスト コードでサポートされる型をいくつかの 1 つとして x。 たとえば、ご覧のとおり、int と、WEX::Common::String の両方として取得すること。

```cpp
                int x = 0;
                String xString;
                RuntimeParameters::TryGetValue(L"x", x);
                RuntimeParameters::TryGetValue(L"x", xString);
```

詳細については、次を参照してください、 [TAEF します。ランタイム パラメーター](runtime-parameters.md)ヘルプ ページ。

### <a name="parallel"></a>並列/

複数のプロセッサ全体には、並列でテストを実行します。 テストする必要がありますにオプトイン並列実行で 'Parallel' のメタデータでマークされています。

`te.exe test1.dll /parallel`

詳細については、次を参照してください、[並列](parallel.md)ヘルプ ページ。

### <a name="persistpictresults"></a>/persistPictResults

使用してテスト用 PICT.exe によって生成される結果をキャッシュ[PICT DataSource](pict-data-source.md)現在の実行にします。 後続のテストの実行は、同じモデル ファイルとシード ファイルに対して PICT.exe を実行している操作と同じようにキャッシュされた結果を利用しようとします。

### <a name="pictoptionnameoptionvalue"></a>/pict:\<OptionName>=\<OptionValue>

オプションは、使用してテストを制御する PICT.exe で呼び出されたときに、 [PICT DataSource](pict-data-source.md)します。 現在これらのオプションのいずれかを設定すると、コードに関連付けられているすべてのメタデータが上書きされます。 次のオプションが使用できます。

/Pict:Order=3  
PICT.exe の/o コマンド オプションを使用して、値を渡すことによって、組み合わせの順序を設定します。

/Pict:ValueSeparator=;  
PICT.exe の/d コマンド オプションを使用して、値を渡すことによって、値の区切り記号を設定します。

/Pict:AliasSeparator=+  
PICT.exe の/a コマンド オプションを使用して、値を渡すことによって、エイリアスの区切り記号を設定します。

Pict: NegativeValuePrefix =!  
PICT.exe の/n コマンド オプションを使用して、値を渡すことによって、負の値のプレフィックスを設定します。

/Pict:SeedingFile=test.seed  
PICT.exe の/e コマンド オプションを使用して、値を渡すことによってシード処理のファイルへのパスを設定します。

/Pict:Random=true  
有効または無効 PICT 結果の乱数性能、PICT データ ソースを使用したランダム シードをログにします。

/Pict:RandomSeed=33  
PICT.exe の/r コマンド オプションを使用して、値を渡すことによって、ランダム シードを設定します。 Pict は、この設定が有効になります: ランダムな場合を除き、Pict: ランダムが明示的に false に設定します。

/Pict:CaseSensitive=true  
True の場合、有効に設定すると PICT.exe に/c コマンドのオプションを渡すことで大文字小文字の区別にします。

/Pict:Timeout=00:01:30  
PICT.exe が完了するまでそのプロセスを強制終了を待機する時間を設定します。 値の形式が\[日\]。1 時間\[: 分\[: 2 つ目\[します。FractionalSeconds\]\]\]します。

### <a name="runasrunastype"></a>/runas:\<RunAsType >

指定された環境でテストを実行します。 参照してください、 [RunAs](runas.md)使用状況の詳細については、ドキュメント。

te.exe \*.dll/runas:System  

**解釈します。** システムとして、すべてのテストを実行します。

te.exe \*.dll/runas:Elevated  

**解釈します。** 管理者特権でのユーザーとして、すべてのテストを実行します。

te.exe \*.dll/runas: 制限  

**解釈します。** 非管理者の特権ユーザーとして、すべてのテストを実行します。

te.exe \*.dll /runas:LowIL  

**解釈します。** 低い整合性プロセスでは、すべてのテストを実行します。

### <a name="runignoredtests"></a>/runIgnoredTests

実行するかを示します (と共に場合[/list](#list)または[/listProperties](#listproperties)) など、すべてのテストはテスト クラスと、"true"に「無視」のメタデータ セットを持つメソッドをテストします。 既定のテスト クラスとテストによって"true"に「無視」のメタデータ セットを持つメソッドは一覧中や実行中にスキップされます。

### <a name="runonmachinename"></a>/runon:\<MachineName>

指定されたコンピューターにリモートでテストを実行します。 TAEF で認証し承認、テストを実行するために必要なバイナリを展開し、元のコンソールに戻り、すべての情報を記録します。 参照してください、[クロス マシンのテストの実行](cross-machine-execution.md)使用状況の詳細については、ドキュメント。

te.exe \*.dll /runon:TestMachine1

**解釈します。** "TestMachine1"のすべてのテストをリモートで実行します。

### <a name="selectquery"></a>/select:\<query>

各テストを選択するときに使用される選択条件では、バイナリをテストします。 選択基準は、次の 1 つ以上で構成されます。

@\[プロパティ名\] = \[値を文字列として\]
@\[プロパティ名\] &gt; = \[値を浮動小数点または整数として\] 
@\[プロパティ名\] &gt; \[値を浮動小数点または整数として\]
@\[プロパティ名\] &lt;= \[値を浮動小数点または整数として\]
@\[プロパティ名\] &lt; \[と浮動小数点または整数値\]

* *プロパティ値を文字列としては、単一引用符で囲んである必要があります。*
* *使用して複合選択条件を指定する「および」,「または」、"not"(大文字と小文字は区別されません)。*
* *プロパティの文字列値を使用してワイルドカード文字はサポート"\*「と」?"文字です。*
* *浮動小数点と整数の値を"\*"文字は、'exists' が、部分一致では使用できませんにも使用可能性があります。* 例:**選択/:"@Priority=\*"** 有効ですが**選択/:"@Priority= 4\*"** はありません。

te.exe test1.dll リンク:"(@Name='\*TestToLower' または@Owner= 'C2') および not (@Priority &lt; 3)"

**解釈します。** メソッド名が 'TestToLower' または 'C2'; の所有者を終了 test1.dll ですべてのテストを実行します。優先順位が 3 未満ではありません。

te.exe test1.dll test2.dll /select:@Priority=\*

**解釈します。** テスト メタデータで優先順位が指定されている test1.dll と test2.dll ですべてのテストを実行します。

te.exe test1.dll /select:@Name='\*StringTest\*'  

**解釈します。** その名前空間、クラスまたはメソッド名に 'StringTest' test1.dll という語句を含むすべてのテストを実行します。

### <a name="sessiontimeoutvalue"></a>/sessionTimeout:\<値 >

Te.exe の実行全体のセッションのタイムアウトを設定します。 タイムアウトに達すると、テスト セッションが正常に中止され、プロセス終了コードは、タイムアウトが発生したことを示します。

> [!NOTE]
> タイムアウト値は、次の形式で指定する必要があります。

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]]
```

> [!NOTE]
> WTT、実行されている場合、TAEF セッションがタイムアウトになる場合でも、Wtt のログ ファイルがそのまま保たれるようにするこの値を使用できます。

te.exe test1.dll/sessionTimeout:0:0:0.5  

テスト全体のセッションは、.5 秒後にタイムアウトします。

te.exe test1.dll /sessionTimeout:0:0:45  

テスト全体のセッションは 45 秒後にタイムアウトになります。

te.exe test1.dll /sessionTimeout:0:20  

テスト全体のセッションが 20 分後にタイムアウトになります。

te.exe test1.dll/sessionTimeout:5  

テスト全体のセッションが 5 時間後にタイムアウトになります。

te.exe test1.dll/sessionTimeout:1.2  

テスト全体のセッションが 1 日 2 時間後にタイムアウトになります。

### <a name="terminateonfirstfailure"></a>/terminateOnFirstFailure

テストのテスト エラーが発生した初めての実行を終了します。 そのテストのすべての破棄操作が呼び出されますが、後続のすべてのテストが無視とマークされます。 既知の問題により、テストがテスト モードを使用するときに実行を続ける可能性があります。

`te.exe test1.dll /terminateOnFirstFailure`

### <a name="testdependenciesfiles"></a>/testDependencies:\<ファイル >

デプロイを使用する場合に、追加のテストの依存関係を指定[マシンのテストの実行をクロス](cross-machine-execution.md)します。 完全なパスを指定しない限り、テスト ディレクトリではなく、現在のディレクトリを基準 TAEF が検索されます。

te.exe \*.dll /runon:TestMachine1 /TestDependencies:test\*.jpg;file1.doc  

**解釈します。** "TestMachine1"でコピー、すべてのテストをリモートで実行 ' テスト\*.jpg' と 'file1.doc' 経由で任意のテストを実行する前に、リモート コンピューターにします。 各ファイルの仕様は、ワイルドカード文字を含めることができます (test.txt; テスト\*.dll など) を 1 つまたは複数のファイルと一致します。

### <a name="testtimeoutvalue"></a>/testTimeout:\<値 >

Te.exe の実行全体のグローバルのテストのタイムアウトを設定します。 この値には、いずれかがよりも優先[テスト タイムアウト](standard-test-metadata.md)メタデータが実行されている指定されたテストの設定されている可能性があります。

> [!NOTE]
> タイムアウト値は、次の形式で指定する必要があります。

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]]
```

> [!NOTE]
> 組み合わせて使用する場合は無視されます[/inproc](#inproc)します。

te.exe test1.dll/testTimeout:0:0:0.5  

すべてのテストとセットアップ/クリーンアップ メソッドは、.5 秒後にタイムアウトします。

te.exe test1.dll /testTimeout:0:0:45  

すべてのテストとセットアップ/クリーンアップ メソッドは、45 秒後にタイムアウトします。

te.exe test1.dll /testTimeout:0:20  

すべてのテストとセットアップ/クリーンアップ メソッドは、20 分後にタイムアウトします。

te.exe test1.dll/testTimeout:5  

すべてのテストとセットアップ/クリーンアップ メソッドは 5 時間後にタイムアウトになります。

te.exe test1.dll/testTimeout:1.2  

すべてのテストとセットアップ/クリーンアップ メソッドは、1 日 2 時間後にタイムアウトします。

### <a name="unicodeoutputtruefalse"></a>/unicodeOutput:\<true/false>

TE は、テキスト ファイルにパイプされます、ときに、既定で unicode を出力します。 1 つの例外は、既存の ANSII ファイルに追加することが要求かどうか (を使用して '&gt;&gt;')。

この動作をオーバーライドするには/unicodeOutput:false を指定することがあります。 これで、TE ANSII をファイルに常に出力します。

`te.exe test1.dll /unicodeOutput:false > output.txt`

## <a name="logger-settings"></a>ロガーの設定

### <a name="appendwttlogging"></a>/appendWttLogging

WTT ログ記録が有効な場合は、上書きするのではなく、ログ ファイルに追加します。 組み合わせて使用する必要があります[/enableWttLogging](#enablewttlogging)します。

te.exe test1.dll /enableWttLogging /appendWttLogging  

作成、またはという名前のログ ファイルに追加されます*TE.wtl*テストの実行が完了します。

### <a name="enablewttlogging"></a>/enableWttLogging

WTT; のログ記録を有効にします。Wttlog.dll は、パスで使用可能なである必要があります。

te.exe test1.dll/enableWttLogging

という名前のログ ファイルが生成されます*TE.wtl*テストの実行が完了します。

### <a name="defaultappdomain"></a>/defaultAppDomain

既定のアプリケーション ドメインでは、管理対象のテストを実行します。

te.exe managed.test1.dll/defaultAppDomain  

### <a name="disableconsolelogging"></a>/disableConsoleLogging

コンソール ログ出力を無効にします。組み合わせて使用する必要があります[/enableWttLogging](#enablewttlogging)します。

`te.exe test1.dll /disableConsoleLogging /enableWttLogging`

### <a name="logfilename"></a>/logFile:\<name>

Wtt ログ ファイルとして使用する名前を指定します。組み合わせて使用する必要があります[/enableWttLogging](#enablewttlogging)します。

te.exe test1.dll /logFile:myCustomLogFile.xml /enableWttLogging  

という名前のログ ファイルが生成されます*myCustomeLogFile.xml*テストの実行が完了します。

### <a name="logoutputmode"></a>/logOutput:\<mode>

ロガーの出力レベルを設定します。 有効な値は次のとおりです。

* *高*:すべてのトレースの横にあるタイムスタンプの印刷などの何らかの他のコンソール出力を有効にします。
* *低*:唯一のコア イベント (開始、終了グループなど) とエラーを出力します。 ログ ファイルには、低い優先順位の詳細の前に、エラーのコンテキストを提供するすべてのエラーが含まれます。
* *LowWithConsoleBuffering*:同じ*低*、ログ ファイルとコンソールの出力エラーのコンテキストが含まれています。
* *最も低い*:同じ*低*、コンソール出力には、エラーのみ、テストの失敗、および実行の概要が含まれています。

### <a name="version"></a>/version

詳細なバージョン情報を出力します。

### <a name="wttdevicestringvalue"></a>/wttDeviceString:\<value>

WexLogger WttLogger を初期化するときに使用する WttDeviceString を完全に上書きします。

`te.exe test1.dll /wttDeviceString:$Console`

### <a name="wttdevicestringsuffixvalue"></a>/wttDeviceStringSuffix:\<value>

既定 WttDeviceString WexLogger WttLogger を初期化するときに使用するには、指定した値を追加します。 場合は無視されます[wttDeviceString](#wttdevicestringvalue)も指定します。

`te.exe test1.dll /wttDeviceStringSuffix:$Console`

## <a name="debug-settings"></a>デバッグの設定

### <a name="breakoncreate"></a>/breakOnCreate

各テスト クラスをインスタンス化する前にデバッガーを中断します。

`te.exe test1.dll /breakOnCreate`

### <a name="breakonerror"></a>/breakOnError

エラーまたはテストの失敗が記録された場合は、デバッガーを中断します。

`te.exe test1.dll /breakOnError`

### <a name="breakoninvoke"></a>/breakOnInvoke

各テスト メソッドを呼び出す前にデバッガーを中断します。

`te.exe test1.dll /breakOnInvoke`

### <a name="disabletimeouts"></a>/disableTimeouts

実行中には、すべてのタイムアウトを無効にします。 これはできるデバッグ時は、デバッグ中のプログラム側 TAEF が待機しているときにタイムアウトを防ぐために役立つこと。

`te.exe test1.dll /disableTimeouts`

### <a name="minidumponerror"></a>/miniDumpOnError

テストのエラーまたは障害が発生する場合は、ミニ ダンプをログ記録を受け取り。

`te.exe test1.dll /miniDumpOnError`

### <a name="minidumponcrash"></a>/miniDumpOnCrash

テスト クラッシュが発生した場合に、ミニ ダンプをログ記録を受け取り。

`te.exe test1.dll /miniDumpOnCrash`

### <a name="rebootstatefile"></a>/rebootStateFile

実行を明示的に有効[再起動](reboot.md)テストします。

`te.exe test1.dll /rebootStateFile:myFile.xml`

### <a name="reportloadingissue"></a>/reportLoadingIssue

TAEF がテスト dll の読み込みに失敗したときに、エラーの説明ダイアログが表示されます。 ネイティブ テスト dll の読み込みに関する問題の調査のためにのみ使用する必要があります。

`te.exe test1.dll /reportLoadingIssue`

### <a name="screencaptureonerror"></a>/screenCaptureOnError

テストのエラーや障害が発生した場合、画面キャプチャのログに記録します。

`te.exe test1.dll /screenCaptureOnError`

### <a name="stackframecountvalue"></a>/stackFrameCount:\<value>

呼び出し履歴を取得するときに表示するスタック フレームの数を指定します。 既定値は 50 です。

`te.exe test1.dll /stackFrameCount:100`

### <a name="stacktraceonerror"></a>/stackTraceOnError

テスト エラーや障害が発生した場合は、スタック トレースをログ記録を受け取り。

`te.exe test1.dll /stackTraceOnError`

## <a name="test-modes"></a>テスト モード

### <a name="testmodeloop"></a>/testmode:Loop

により、2 つの変数を使用して実行を制御する*ループ*と*LoopTest*します。

* *ループ*:コントロール全体の実行回数が実行されます。 既定の 1 です。
* *LoopTest*:個々 のテストの実行回数を制御します。 既定の 10 です。

te.exe test1.dll /testmode:Loop  

**解釈します。** Test1.dll 10 回ですべてのテストを実行 (既定値の*LoopTest*)。 全体の実行が 1 回実行 (既定値の*ループ*)。

te.exe test1.dll test2.dll /testmode:Loop /Loop:3 /LoopTest:1  

**解釈します。** 1 回 test1.dll と test2.dll ですべてのテストを実行 (によって決まります*LoopTest*)。 全体の実行 (test1.dll と test2.dll ですべての結合のテスト) を 3 回 - によって決定される実行*ループ*します。

### <a name="testmodestress"></a>/testmode:Stress

'Stress' テスト モードで TAEF はまたはテストを実行、無期限に Ctrl キーを押しながら C キーを入力するまで、WM まで\_閉じるメッセージ TAEF の非表示のウィンドウに送信されます。 組み合わせて/testmode:stress を実行する必要があります[/inproc](#inproc)します。

`te.exe test1.dll /testmode:Stress /inproc`

詳細な情報とこのモードでサポートされているその他のパラメーターは、次を参照してください。[テスト モード](test-modes.md)します。

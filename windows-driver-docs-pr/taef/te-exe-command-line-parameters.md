---
title: Te.exe のコマンド オプション
description: Te.exe のコマンド オプション
ms.assetid: E9A9292D-FA30-410d-9322-BD0F321314F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 502964d420b44ff3a1e89960930ef4d565c0e53b
ms.sourcegitcommit: 69261fa09a48b70a681bec0b4cf7afa8b84c73b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68415096"
---
# <a name="teexe-command-options"></a>Te.exe のコマンド オプション

## <a name="usage"></a>使用方法

**:::no-loc text="te.exe":::** \<[:::no-loc text="test\_binaries":::](#test_binaries)> \[[:::no-loc text="/appendWttLogging":::](#appendwttlogging)\] \[[:::no-loc text="/breakOnCreate":::](#breakoncreate)\] \[[:::no-loc text="/breakOnError":::](#breakonerror)\] \[[:::no-loc text="/breakOnInvoke":::](#breakoninvoke)\] \[[:::no-loc text="/coloredConsoleOutput":::](#coloredconsoleoutputtruefalse) \] \[ [:::no-loc text="/console:flushWrites":::](#consoleflushwrites) \] \[ [ :::no-loc text="/console:position=\[x,y | current"::: \] ](#consolepositionxy--current-) \[ [ :::no-loc text="/console:size=&lt;x,y&gt;"::: \] ](#consolesize-xy--current-) \[ [ :::no-loc text="/console:topmost":::\]](#consoletopmost) [\[:::no-loc text="/defaultAppDomain":::\]](#defaultappdomain) \[[:::no-loc text="/disableConsoleLogging":::](#disableconsolelogging)\] \[[:::no-loc text="/disableTimeouts":::](#disabletimeouts)\] \[[:::no-loc text="/dpiaware":::](#dpiaware) \] \[[:::no-loc text="/enableWttLogging":::](#enablewttlogging) \] \[ [:::no-loc text="/inproc":::](#inproc) \] \[ [:::no-loc text="/isolationLevel":::](#isolationlevellevel) \] \[ [:::no-loc text="/labMode":::](#labmode) \] \[[:::no-loc text="/list":::](#list)\] \[[:::no-loc text="/listProperties":::](#listproperties)\] \[[:::no-loc text="/logFile:&lt;name&gt;":::](#logfilename)\] \[[:::no-loc text="/logOutput:&lt;mode&gt;":::](#logoutputmode)\] \[[:::no-loc text="/miniDumpOnCrash":::](#minidumponcrash)\] \[[:::no-loc text="/miniDumpOnError":::](#minidumponerror)\] \[[:::no-loc text="/name:&lt;testname&gt;":::](#nametestname)\] \[[:::no-loc text="/outputFolder:&lt;folderName&gt;":::](#outputfolderfoldername)\] \[[:::no-loc text="/p:&lt;ParamName&gt;=&lt;ParamValue&gt;":::](#pparamnameparamvalue) \] \[ [:::no-loc text="/parallel":::](#parallel) \] \[ [:::no-loc text="/persistPictResults":::](#persistpictresults) \] \[ [:::no-loc text="/pict:&lt;OptionName&gt;=&lt;OptionValue&gt;":::](#pictoptionnameoptionvalue) \] [ \[:::no-loc text="/rebootStateFile":::\]](#rebootstatefile) \[[:::no-loc text="/reportLoadingIssue":::](#reportloadingissue)\] \[[:::no-loc text="/runas:&lt;RunAsType&gt;":::](#runasrunastype)\] \[[:::no-loc text="/runIgnoredTests":::](#runignoredtests)\]<s></s>

## <a name="selectionexecution-commands"></a>選択/実行コマンド

### <a name="testbinaries"></a>test_binaries

実行する1つ以上のテストファイルを、スペースで区切って指定します。 ワイルドカード文字がサポートされています。

#### <a name="teexe-test1dll"></a>te test1

**割り当てる**Test1 ですべてのテストを実行します。

#### <a name="teexe-test1dll-test2dll-test3dll"></a>al.exe test1 test3 を実行します。

**割り当てる**Test1、test2、および test3 のすべてのテストを実行します。

#### <a name="teexe-dll"></a>\*te .dll

**割り当てる**現在のディレクトリにあるすべての dll のすべてのテストを実行します。

### <a name="coloredconsoleoutputtruefalse"></a>/coloredconsoleoutput:\<true/false >

TAEF が色分けされたコンソールテキストを出力するかどうかを指定します。 既定値は true です。 False に設定すると、TAEF はすべてのテキストを既定のコンソールの色で出力します。

`te.exe test1.dll /coloredConsoleOutput:false`

### <a name="consoleoptionnamevalue"></a>/console:\<optionName > =\<値 >

TE でのコンソールの使用を構成するためのオプションを提供します。 次のオプションを使用できます。

#### <a name="consoleflushwrites"></a>/console: flushWrites

すべての行が書き込まれた後にコンソール出力がフラッシュされるようにします。 .exe の出力がリダイレクトされるときに便利です。

#### <a name="consolepositionxy--current-"></a>/console: position =\[x、y | current\]

プライマリモニターの隅を基準とした、コンソールウィンドウの位置 (ピクセル単位) を設定します。 **[現在]** の値を使用して、再起動から再開するときに現在のコンソールの位置を保存して使用するように指定します。

#### <a name="consolesize-ltxygt--current-"></a>/console: size =\[ &lt;x、y&gt; | current\]

コンソールウィンドウのサイズを文字単位で設定します。 必要に応じて、ウィンドウのサイズに合わせて画面バッファーサイズが増加します。 Current**の値**を使用して、再起動から再開するときに現在のコンソールサイズを格納して使用することを指定します。

#### <a name="consoletopmost"></a>/console: 最上位

実行中は、コンソールをデスクトップの z オーダーで実行中の状態のままにしておきます。

### <a name="dpiaware"></a>/dpiaware

DPI 対応のマークが付いたプロセスでテストを実行します。「[高 DPI](https://docs.microsoft.com/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)」を参照してください。 これは、メタデータ ("DpiAware") を使用して設定することもできます。

### <a name="inproc"></a>/inproc

Te 内ではなく、al.exe プロセス内ですべてのテストを実行します。ProcessHost。

te test1/inproc

> [!NOTE]
> TE は、 */inproc*設定を使用するときに、一度に1つのテスト dll の実行のみをサポートします。

### <a name="isolationlevellevel"></a>/isolationLevel:\<レベル >

TAEF テストの実行時に使用される分離の最小レベルを指定します。 この値がメタデータとして指定された IsolationLevel と競合する場合、値は強力なスコープと分離レベルになります。 詳細については、「[テスト分離](test-isolation.md)」を参照してください。

`te.exe test1.dll /isolationLevel:Class`

### <a name="labmode"></a>/labmode

テストを実行し、潜在的なブロッキング UI (たとえば、クラッシュしたテストの Windows エラー報告ダイアログ) を削除します。

### <a name="list"></a>/list

すべての[テスト\_バイナリ](#test_binaries)の名前とその中のクラスとメソッドの一覧を表示します。 選択条件が指定されている場合は、条件を満たす名前だけが一覧表示されます。

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

すべてのテスト\_バイナリの名前とプロパティ、およびそれらのクラスとメソッドを、セットアップおよび破棄の関数名 (使用可能な場合) と共に一覧表示します。 選択条件が指定されている場合は、条件を満たす名前だけが一覧表示されます。

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

### <a name="nametestname"></a>/name:\<testname >

テスト名に基づく選択は、"/select:@Name= '&lt;testname&gt;'" に代わる簡単な方法です。 Testname &lt;\*には、ワイルドカード文字 ("" および "?") を含めることができますが、単一引用符で囲むことはできません。&gt; コマンドプロンプトで/select と/name both の両方を指定した場合、/select クエリが優先され、/name は無視されます。

te test1/name:\*TestToLower  

**割り当てる**Test1 で、メソッド名が ' TestToLower ' で終わるすべてのテストを実行します。 同じを、選択基準を使用して/select:@Name= '\*TestToLower ' として表すことができます。

te test1/name:\*stringtest\*  

**割り当てる**名前空間、クラス、またはメソッド名に ' StringTest ' という語句が含まれている、test1 内のすべてのテストを実行します。

### <a name="outputfolderfoldername"></a>/outputfolder:\<folderName >

生成されたすべてのファイルを配置するフォルダーを指定します。 既定値は、現在のディレクトリです。 環境変数を使用できます。次に例を示します。

`te.exe test1.dll /outputFolder:%TEMP%\\MyOutput`

### <a name="pparamnameparamvalue"></a>/p:\<ParamName > =\<ParamValue >

パラメーター名 = ParamName とパラメーター値 = ParamValue のランタイムパラメーターを定義します。 これらのパラメーターには、テストメソッドまたはセットアップ/クリーンアップメソッドからアクセスできます。

`te.exe test1.dll /p:x=5 /p:myParm=cool`

テストコードでサポートされているいくつかの型の1つとして x を取得できます。 たとえば、次のように、int と WEX:: Common:: String の両方として取得することができます。

```cpp
                int x = 0;
                String xString;
                RuntimeParameters::TryGetValue(L"x", x);
                RuntimeParameters::TryGetValue(L"x", xString);
```

詳細については、Taef にアクセスしてください[。ランタイムパラメーター](runtime-parameters.md)のヘルプページ。

### <a name="parallel"></a>/parallel

複数のプロセッサにわたって並列でテストを実行します。 テストで並列実行をオプトインするには、' Parallel ' メタデータでマークされている必要があります。

`te.exe test1.dll /parallel`

詳細については、[並列](parallel.md)ヘルプページを参照してください。

### <a name="persistpictresults"></a>/persisttitresults

現在の実行で[Pict データソース](pict-data-source.md)を使用しているテストのために、pict によって生成された結果をキャッシュします。 その後のテスト実行では、同じモデルおよびシードファイルに対して PICT を実行するのと同じように、キャッシュされた結果を使用しようとします。

### <a name="pictoptionnameoptionvalue"></a>/pict:\<OptionName > =\<OptionValue >

Pict[データソース](pict-data-source.md)を使用してテスト用に呼び出された場合に、pict を制御するオプションを提供します。 これらのオプションのいずれかを設定すると、コード内の関連するすべてのメタデータが上書きされます。 次のオプションを使用できます。

/Pict: 順序 = 3  
の値を使用して、組み合わせの順序を設定する、/o コマンドオプションを指定します。

/Pict: ValueSeparator =;  
PICT の/d コマンドオプションを使用して値を渡して、値の区切り記号を設定します。

/Pict: 別名区切り記号 = +  
PICT の/a コマンドオプションを使用して値を渡すことによって、エイリアスの区切り記号を設定します。

Pict: NegativeValuePrefix =!  
PICT の/n コマンドオプションを使用して値を渡すことによって、負の値のプレフィックスを設定します。

/Pict: SeedingFile = test. seed  
PICT の/e コマンドオプションを使用して値を渡すことにより、シード処理ファイルへのパスを設定します。

/Pict: Random = true  
PICT の結果をランダムにオンまたはオフにし、使用されたランダムシードを PICT データソースログに記録します。

/Pict: RandomSeed = 33  
PICT の/r コマンドオプションを使用して値を渡すことによって、ランダムシードを設定します。 このオプションを設定すると、pict: Random が明示的に false に設定されていない限り、Pict が有効になります。

/Pict: CaseSensitive = true  
True に設定すると、/c コマンドオプションを PICT に渡すことによって、大文字小文字の区別が有効になります。

/Pict: Timeout = 00:01:30  
プロセスを強制終了する前に、PICT が終了するまで待機する時間を設定します。 値の形式\[は Day です。\]時\[: 分\[: 秒\[。FractionalSeconds\]。\]\]

### <a name="runasrunastype"></a>/runas:\<runastype >

指定された環境でテストを実行します。 使用方法の詳細については、 [RunAs](runas.md)のドキュメントを参照してください。

\*te .dll/runas: System  

**割り当てる**すべてのテストをシステムとして実行します。

te .dll/runas: 昇格された\*  

**割り当てる**すべてのテストを管理者特権を持つユーザーとして実行します。

\*te .dll/runas: 制限付き  

**割り当てる**すべてのテストを、管理者特権ではないユーザーとして実行します。

\*te .dll/runas: lowil  

**割り当てる**低整合性プロセスですべてのテストを実行します。

### <a name="runignoredtests"></a>/runignoredtests

"Ignore" メタデータが "true" に設定されたテストクラスとテストメソッドを含む、またはリスト ( [/list](#list)または[/listProperties](#listproperties)と組み合わせて使用する場合) を実行します。 既定では、"Ignore" メタデータが "true" に設定されているテストクラスとテストメソッドは、実行中および一覧表示中にスキップされます。

### <a name="runonmachinename"></a>/runon:\<MachineName >

指定されたコンピューターでテストをリモートで実行します。 TAEF は、テストを実行するために必要なバイナリを認証、承認、および展開し、すべての情報を元のコンソールに記録します。 使用方法の詳細については、[クロスマシンのテスト実行](cross-machine-execution.md)に関するドキュメントを参照してください。

\*te .dll/runon: TestMachine1

**割り当てる**"TestMachine1" ですべてのテストをリモートで実行します。

### <a name="selectquery"></a>/select:\<クエリ >

各テストバイナリからテストを選択するときに使用する選択条件。 選択条件は、次の1つ以上で構成されます。

@\[プロパティ名\]\]の値\[を文字列プロパティ名
@の値&gt;として float または integer として指定\]  = \[\[ = \]\[\] floatまた&lt;は整数&gt; のプロパティ\]名としてのプロパティ名の値\]
@ 
@ \[\[ = 
@ floatまた&lt;は integer 型\]の\[プロパティ名\]値と\[しての値\[\]

* *文字列としてのプロパティ値は、単一引用符で囲む必要があります。*
* *複合選択条件は、"and"、"or"、および "not" を使用して指定できます (大文字と小文字は区別されません)。*
* *プロパティ文字列値は、"\*" および "?" 文字を使用したワイルドカード文字をサポートしています。*
* *Float 型と整数型の値の\*場合、"" という文字を ' exists ' として使用することもできますが、部分一致に使用することはできません。* 例: **/select: "@Priority\*="** は有効ですが、 **/select: "@Priority= 4\*"** は有効ではありません。

te test1@Name/select: "(= '\*TestToLower ' or @Owner= ' c2 ') and not (@Priority &lt; 3)"

**割り当てる**Test1 内のすべてのテストを実行します。メソッド名の末尾が ' TestToLower ' であるか、所有者が ' C2 ' です。ここで、Priority は3未満ではありません。

al.exe test1 (test2 /select:@Priority) =\*

**割り当てる**テストメタデータに優先順位が指定されている test1 および test2 のすべてのテストを実行します。

te test1 /select:@Name= '\*stringtest\*'  

**割り当てる**名前空間、クラス、またはメソッド名に ' StringTest ' という語句が含まれている、test1 内のすべてのテストを実行します。

### <a name="sessiontimeoutvalue"></a>/sessionTimeout:\<値 >

Al.exe の実行全体に対してセッションタイムアウトを設定します。 タイムアウトが経過すると、テストセッションは正常に中止され、プロセス終了コードはタイムアウトが発生したことを示します。

> [!NOTE]
> タイムアウト値は、次の形式で指定する必要があります。

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]]
```

> [!NOTE]
> WTT の下で実行されている場合、この値を使用して、TAEF セッションがタイムアウトした場合でも Wtt ログファイルがそのまま維持されるようにすることができます。

te test1/sessionTimeout: 0: 0: 0.5  

テストセッション全体は、5秒後にタイムアウトします。

te test1/sessionTimeout: 0: 0:45  

テストセッション全体は、45秒後にタイムアウトします。

te test1/sessionTimeout: 0:20  

テストセッション全体は、20分後にタイムアウトします。

te test1/sessionTimeout: 5  

テストセッション全体は、5時間後にタイムアウトします。

te test1/sessionTimeout: 1.2  

テストセッション全体は、1日と2時間後にタイムアウトします。

### <a name="terminateonfirstfailure"></a>/terminateOnFirstFailure

テストの失敗が初めて発生したときに、テストの実行を終了します。 そのテストのすべての破棄操作が呼び出されますが、後続のすべてのテストは無視済みとしてマークされます。 既知の問題により、テストモードの使用時にテストが引き続き実行される可能性があります。

`te.exe test1.dll /terminateOnFirstFailure`

### <a name="testdependenciesfiles"></a>/testDependencies:\<ファイル >

[クロスマシンテストの実行](cross-machine-execution.md)を使用するときに配置する追加のテスト依存関係を指定します。 完全なパスが指定されていない限り、TAEF はテストディレクトリではなく、現在のディレクトリを基準として検索します。

te .dll/runon: TestMachine1/TestDependencies\*: test.txt; file1. doc \*  

**割り当てる**"TestMachine1" ですべてのテストをリモートで実行し、\*テストを実行する前に ' test.txt ' と ' file1 ' をリモートコンピューターにコピーします。 各ファイルの指定には、1つ以上のファイルに\*一致するワイルドカード文字 (test.txt、test .dll など) を含めることができます。

### <a name="testtimeoutvalue"></a>/testTimeout:\<値 >

Al.exe の実行全体のグローバルテストタイムアウトを設定します。 この値は、実行されている特定のテストに対して設定されている可能性がある[テストタイムアウト](standard-test-metadata.md)メタデータをオーバーライドします。

> [!NOTE]
> タイムアウト値は、次の形式で指定する必要があります。

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]]
```

> [!NOTE]
> [/](#inproc)と共に使用すると、は無視されます。

te test1/testTimeout: 0: 0: 0.5  

すべてのテストおよびセットアップ/クリーンアップメソッドは、5秒後にタイムアウトします。

te test1/testTimeout: 0: 0:45  

すべてのテストとセットアップ/クリーンアップの方法は、45秒後にタイムアウトになります。

te test1/testTimeout: 0:20  

すべてのテストとセットアップ/クリーンアップの方法は、20分後にタイムアウトになります。

te test1/testTimeout: 5  

テストとセットアップ/クリーンアップの各メソッドは、5時間後にタイムアウトします。

te test1/testTimeout: 1.2  

テストとセットアップ/クリーンアップの各メソッドは、1日と2時間後にタイムアウトします。

### <a name="unicodeoutputtruefalse"></a>/unicodeOutput:\<true/false >

TE がテキストファイルにパイプされると、既定で unicode が出力されます。 この例外は、('&gt;&gt;' 経由で) 既存の ANSII ファイルに追加するように要求した場合です。

この動作をオーバーライドするには、/unicodeOutput: false を指定します。 これにより、TE は常に ANSII をファイルに出力します。

`te.exe test1.dll /unicodeOutput:false > output.txt`

## <a name="logger-settings"></a>Logger の設定

### <a name="appendwttlogging"></a>/appendWttLogging

WTT ログ記録が有効になっていると、は上書きするのではなく、ログファイルにを追加します。 [/EnableWttLogging](#enablewttlogging)と組み合わせて使用する必要があります。

te test1/enableWttLogging/appendWttLogging  

テストの実行が完了すると、が作成されるか、または拡張子がのログファイルに追加されます。

### <a name="enablewttlogging"></a>/enableWttLogging

WTT ログ記録を有効にします。Wttlog はパスで使用できる必要があります。

te test1/enableWttLogging

テスト実行の完了時に、" *TE* " というログファイルが生成されます。

### <a name="defaultappdomain"></a>/defaultappdomain

既定のアプリケーションドメインでマネージテストを実行します。

al.exe 管理されている .exe/defaultappdomain  

### <a name="disableconsolelogging"></a>/disablecon? ログ

コンソールのログ出力を無効にします。[/enableWttLogging](#enablewttlogging)と組み合わせて使用する必要があります。

`te.exe test1.dll /disableConsoleLogging /enableWttLogging`

### <a name="logfilename"></a>/logFile:\<名前 >

Wtt ログファイルとして使用する名前を指定します。[/enableWttLogging](#enablewttlogging)と組み合わせて使用する必要があります。

te test1/logFile: myCustomLogFile .xml/enableWttLogging  

テスト実行の完了時に、 *myCustomeLogFile*というログファイルが生成されます。

### <a name="logoutputmode"></a>/logoutput:\<モード >

Logger の出力レベルを設定します。 有効な値は、

* *高*:すべてのトレースの横にタイムスタンプを印刷するなど、追加のコンソール出力を有効にします。
* *低*:コアイベント (開始、終了グループなど) およびエラーのみを出力します。 ログファイルには、エラーのコンテキストを提供するためにエラーが発生する前の優先度の低い詳細が含まれます。
* *Lowwithconsolebuffering*:*低*と同じですが、ログファイルとコンソールの両方の出力にエラーのコンテキストが含まれています。
* *最低*:[*低*] と同じですが、コンソールの出力には、エラー、テストの失敗、および実行の概要が含まれます。

### <a name="version"></a>/version

詳細なバージョン情報を出力します。

### <a name="wttdevicestringvalue"></a>/wttDeviceString:\<値 >

WttLogger を初期化するときに、WexLogger によって使用される WttDeviceString を完全にオーバーライドします。

`te.exe test1.dll /wttDeviceString:$Console`

### <a name="wttdevicestringsuffixvalue"></a>/wttDeviceStringSuffix:\<値 >

指定された値を、WexLogger が WttLogger を初期化するときに使用する既定の WttDeviceString に追加します。 [WttDeviceString](#wttdevicestringvalue)も指定されている場合は無視されます。

`te.exe test1.dll /wttDeviceStringSuffix:$Console`

## <a name="debug-settings"></a>デバッグ設定

### <a name="breakoncreate"></a>/breakOnCreate

各テストクラスをインスタンス化する前に、デバッガーを中断します。

`te.exe test1.dll /breakOnCreate`

### <a name="breakonerror"></a>/breakonerror

エラーまたはテストの失敗がログに記録された場合に、デバッガーを中断します。

`te.exe test1.dll /breakOnError`

### <a name="breakoninvoke"></a>/breakoninvoke

各テストメソッドを呼び出す前に、デバッガーを中断します。

`te.exe test1.dll /breakOnInvoke`

### <a name="disabletimeouts"></a>/disableタイムアウト

実行中のすべてのタイムアウトを無効にします。 これは、デバッグ中にデバッグ中のプログラムの一部で TAEF が待機しているときにタイムアウトが発生しないようにする場合に便利です。

`te.exe test1.dll /disableTimeouts`

### <a name="minidumponerror"></a>/miniDumpOnError

テストエラーまたはエラーが発生した場合は、ミニダンプを取得してログに記録します。

`te.exe test1.dll /miniDumpOnError`

### <a name="minidumponcrash"></a>/miniDumpOnCrash

テストクラッシュが発生した場合は、ミニダンプを取得してログに記録します。

`te.exe test1.dll /miniDumpOnCrash`

### <a name="rebootstatefile"></a>/rebootStateFile

[再起動](reboot.md)テストの実行を明示的に有効にします。

`te.exe test1.dll /rebootStateFile:myFile.xml`

### <a name="reportloadingissue"></a>/reportloadingissue

TAEF がテスト dll の読み込みに失敗した場合に、エラーの説明のダイアログを表示します。 ネイティブテスト dll の読み込みに関する問題を調査する場合にのみ使用してください。

`te.exe test1.dll /reportLoadingIssue`

### <a name="screencaptureonerror"></a>/screenCaptureOnError

テストエラーまたはエラーが発生した場合に、画面キャプチャを取得してログに記録します。

`te.exe test1.dll /screenCaptureOnError`

### <a name="stackframecountvalue"></a>/stackframecount:\<値 >

呼び出し履歴を取得するときに表示するスタックフレームの数を指定します。 既定値は 50 です。

`te.exe test1.dll /stackFrameCount:100`

### <a name="stacktraceonerror"></a>/stacktraceonerror

テストエラーまたはエラーが発生した場合は、スタックトレースを取得してログに記録します。

`te.exe test1.dll /stackTraceOnError`

## <a name="test-modes"></a>テスト モード

### <a name="testmodeloop"></a>/testmode: Loop

2つの変数*Loop*と*LoopTest*を使用して実行を制御できます。

* *ループ*:実行全体を実行する回数を制御します。 既定値は1です。
* *LoopTest*:個々のテストを実行する回数を制御します。 既定値は10です。

te test1/testmode: Loop  

**割り当てる**Test1 内のすべてのテストを10回実行します ( *LoopTest*の既定値)。 実行全体が1回だけ実行されます (*ループ*の既定値)。

/testmode: Loop/loop: 3/LoopTest: 1 のようになります。  

**割り当てる**Test1 と test2 のすべてのテストを1回実行します ( *LoopTest*によって決定されます)。 実行全体 (test1 と test2 のすべての組み合わせのテスト) は、*ループ*によって決定される3回実行されます。

### <a name="testmodestress"></a>/testmode: ストレス

' ストレス ' テストモードでは、Ctrl + C キーが入力されるか、または WM\_CLOSE メッセージが taef の非表示ウィンドウに送信されるまで、taef はテストを無期限に実行します。 /testmode: ストレスは、 [/inproc](#inproc)と組み合わせて実行する必要があります。

`te.exe test1.dll /testmode:Stress /inproc`

このモードでサポートされている詳細情報とその他のパラメーターについては、「[テストモード](test-modes.md)」を参照してください。

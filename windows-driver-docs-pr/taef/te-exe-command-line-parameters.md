---
title: Te.exe のコマンド オプション
description: Te.exe のコマンド オプション
ms.assetid: E9A9292D-FA30-410d-9322-BD0F321314F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc6d04e11e82734dd00eac0ed24269f8d93fae5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350103"
---
# <a name="teexe-command-options"></a>Te.exe のコマンド オプション


-   [使用状況](#usage)
-   [選択/実行コマンド](#selectionexecutioncommands)
-   [ロガーの設定](#loggersettings)
-   [デバッグの設定](#debugsettings)
-   [テスト モード](#testmodes)

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


**te.exe** &lt;[テスト\_バイナリ](#testbinaries)&gt; \[ [/appendWttLogging](#appendwttlogging) \] \[ [/breakOnCreate](#breakoncreate) \] \[ [/breakOnError](#breakonerror) \] \[ [/breakOnInvoke](#breakoninvoke) \] \[ [/coloredConsoleOutput](#coloredconsoleoutput) \] \[ [/console:flushWrites](#console-option) \] \[ /console:position =&lt;x, y&gt; \] \[ /console:size =&lt;x, y&gt; \] \[ /console: 最上位\] [ \[/defaultAppDomain\]](#defaultappdomain) \[ [/disableConsoleLogging](#disableconsolelogging) \] \[ [/disableTimeouts](#disabletimeouts) \] \[ [/dpiaware](#dpiaware) \] \[ [/enableWttLogging](#enablewttlogging) \] \[ [/inproc](#inproc) \] \[ [/isolationLevel](#isolationlevel) \] \[ [/labMode](#labmode) \] \[ [/list](#list) \] \[ [/listProperties](#listproperties) \] \[ [/logFile:&lt;名前&gt;](#logfile) \] \[ [/logOutput:&lt;モード&gt;](#logoutput) \] \[ [/miniDumpOnCrash](#minidumponcrash) \] \[ [/miniDumpOnError](#minidumponerror) \] \[ [/name:&lt;testname&gt; ](#name) \] \[ [/outputFolder:&lt;folderName&gt; ](#outputfolder) \] \[ [/p:&lt;ParamName&gt;=&lt;ParamValue&gt; ](#p) \]\[<span class= class=""></span class=>&gt;](#wttdevicestringsuffix)\]

## <a name="span-idselectionexecutioncommandsspanspan-idselectionexecutioncommandsspanspan-idselectionexecutioncommandsspanselectionexecution-commands"></a><span id="SelectionExecutionCommands"></span><span id="selectionexecutioncommands"></span><span id="SELECTIONEXECUTIONCOMMANDS"></span>選択/実行コマンド


### <a name="testbinaries"></a>テスト\_バイナリ

(スペースで区切られた) を実行する 1 つまたは複数のテスト ファイルを指定します。 ワイルドカード文字がサポートされています。

<span id="te.exe_test1.dll"></span><span id="TE.EXE_TEST1.DLL"></span>te.exe test1.dll  
**解釈します。** Test1.dll ですべてのテストを実行します。

<span id="te.exe_test1.dll_test2.dll_test3.dll"></span><span id="TE.EXE_TEST1.DLL_TEST2.DLL_TEST3.DLL"></span>te.exe test1.dll test2.dll test3.dll  
**解釈します。** Test1.dll、test2.dll test3.dll ですべてのテストを実行します。

<span id="te.exe__.dll"></span><span id="TE.EXE__.DLL"></span>te.exe \*.dll  
**解釈します。** 現在のディレクトリ内のすべての dll では、すべてのテストを実行します。

### <a name="span-idcoloredconsoleoutputspanspan-idcoloredconsoleoutputspanspan-idcoloredconsoleoutputspancoloredconsoleoutputlttruefalsegt"></a><span id="coloredConsoleOutput"></span><span id="coloredconsoleoutput"></span><span id="COLOREDCONSOLEOUTPUT"></span>/coloredConsoleOutput:&lt;true または false&gt;

TAEF が色付きのコンソールのテキストを出力するかどうかを指定します。 既定値は true です。 False に設定する TAEF はコンソールの既定の色ですべてのテキストを出力します。

**te.exe test1.dll/coloredConsoleOutput:false**

### <a name="span-idconsoleoptionspanspan-idconsoleoptionspanconsoleltoptionnamegtltvaluegt"></a><span id="console_option"></span><span id="CONSOLE_OPTION"></span>/console:&lt;optionName&gt;=&lt;value&gt;

コンソールの TE の使用を構成するためのオプションを提供します。 次のオプションが使用できます。

<span id="console-option"></span>**/console:flushWrites**  
により、コンソール出力は、フラッシュ TE.exe の出力がリダイレクトされたときにすべての行が書き込まれた - に有効です。

<span id="_console_position__x_y___current__"></span><span id="_CONSOLE_POSITION__X_Y___CURRENT__"></span>**/console:position=\[x,y | current \]**  
プライマリ モニター上隅に対して相対的にコンソール ウィンドウの位置をピクセル単位で設定します。 値を使用して、**現在**コンソールの現在の位置を格納されているし、再起動から再開するときに使用することを指定します。

<span id="_console_size____x_y____current__"></span><span id="_CONSOLE_SIZE____X_Y____CURRENT__"></span>**/console:size=\[ &lt;x,y&gt; | current \]**  
(文字ディメンション) で、コンソール ウィンドウのサイズを設定します。 画面バッファーのサイズは、必要に応じて、ウィンドウのサイズに合わせて増加はします。 値を使用して、**現在**を現在のコンソールのサイズを格納されているし、再起動から再開するときに使用することを指定します。

<span id="_console_topmost"></span><span id="_CONSOLE_TOPMOST"></span>**/console:topmost**  
実行中のデスクトップの z オーダーで ' 最上位' te.exe を実行しているコンソールを保持します。

### <a name="span-iddpiawarespanspan-iddpiawarespandpiaware"></a><span id="dpiaware"></span><span id="DPIAWARE"></span>/dpiaware

プロセスでテストを実行します。 DPI 対応としてマークされると、を参照してください[高 DPI](https://msdn.microsoft.com/library/windows/desktop/dd464646)します。 これは、メタデータ ("DpiAware") を使用して設定できます。

### <a name="span-idinprocspanspan-idinprocspaninproc"></a><span id="inproc"></span><span id="INPROC"></span>/inproc

TE 内ではなく、TE.exe プロセス自体内のすべてのテストを実行します。ProcessHost.exe します。

<span id="te.exe_test1.dll__inproc"></span><span id="TE.EXE_TEST1.DLL__INPROC"></span>te.exe test1.dll/inproc  
**注:** TE が一度に 1 つのテスト dll の実行をサポートしてのみを使用する場合、 */inproc*設定します。

### <a name="span-idisolationlevelspanspan-idisolationlevelspanspan-idisolationlevelspanisolationlevelltlevelgt"></a><span id="isolationLevel"></span><span id="isolationlevel"></span><span id="ISOLATIONLEVEL"></span>/isolationLevel:&lt;レベル&gt;

最小 TAEF テストを実行するときに使用する分離レベルを指定します。 この値は、メタデータとして指定された IsolationLevel と競合している場合は、最も厳しいスコープの分離レベルが値になります。 参照してください[テストの分離](test-isolation.md)の詳細。

**te.exe test1.dll/isolationLevel:Class**

### <a name="span-idlabmodespanspan-idlabmodespanspan-idlabmodespanlabmode"></a><span id="labMode"></span><span id="labmode"></span><span id="LABMODE"></span>/labMode

テストを実行し、潜在的なブロッキング UI (たとえば、Windows エラー報告ダイアログ ボックスでテストをクラッシュ) を削除します。

### <a name="span-idlistspanspan-idlistspanlist"></a><span id="list"></span><span id="LIST"></span>/list

すべての名前を一覧表示、[テスト\_バイナリ](#testbinaries)クラスとそれらに含まれるメソッド。 選択条件が指定されている場合は、条件を満たしているものの名前のみを一覧表示します。

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

### <a name="span-idlistpropertiesspanspan-idlistpropertiesspanspan-idlistpropertiesspanlistproperties"></a><span id="listProperties"></span><span id="listproperties"></span><span id="LISTPROPERTIES"></span>/listProperties

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

### <a name="span-idnamespanspan-idnamespannamelttestnamegt"></a><span id="name"></span><span id="NAME"></span>/name:&lt;testname&gt;

テストのベース名の選択に代わる簡単なは"/select:@Name='&lt;testname&gt;'"です。 &lt;Testname&gt;ワイルドカード文字を含めることができますが ("\*「と」?")、単一引用符で囲んでいないに含まれる必要がありますが、します。 リンクと/name 両方がコマンド プロンプトで指定し、/選択場合は、クエリが優先され、/name は無視されます。

<span id="te.exe_test1.dll__name__TestToLower"></span><span id="te.exe_test1.dll__name__testtolower"></span><span id="TE.EXE_TEST1.DLL__NAME__TESTTOLOWER"></span>te.exe test1.dll/name:\*TestToLower  
**解釈します。** メソッド名がどこで 'TestToLower' で終了 test1.dll ですべてのテストを実行します。 選択条件として使用して同じ表現できる/select:@Name='\*TestToLower'。

<span id="te.exe_test1.dll__name__StringTest_"></span><span id="te.exe_test1.dll__name__stringtest_"></span><span id="TE.EXE_TEST1.DLL__NAME__STRINGTEST_"></span>te.exe test1.dll /name:\*StringTest\*  
**解釈します。** その名前空間、クラスまたはメソッド名に 'StringTest' test1.dll という語句を含むすべてのテストを実行します。

### <a name="span-idoutputfolderspanspan-idoutputfolderspanspan-idoutputfolderspanoutputfolderltfoldernamegt"></a><span id="outputFolder"></span><span id="outputfolder"></span><span id="OUTPUTFOLDER"></span>/outputFolder:&lt;folderName&gt;

生成されたすべてのファイルを配置するフォルダーを指定します。 既定値は現在のディレクトリです。 たとえば、環境変数を使用できます。

**te.exe test1.dll/outputFolder:%TEMP%\\方法について**

### <a name="span-idpspanspan-idpspanpltparamnamegtltparamvaluegt"></a><span id="p"></span><span id="P"></span>/p:&lt;ParamName&gt;=&lt;ParamValue&gt;

パラメーターの名前を持つランタイム パラメーターを定義します。 ParamName とパラメーターの値を = ParamValue を = です。 これらのパラメーターは、テスト メソッドまたはセットアップ/クリーンアップのメソッドからアクセスできます。

**te.exe test1.dll /p:x=5 /p:myParm=cool**

取得することができます、テスト コードでサポートされる型をいくつかの 1 つとして x。 たとえば、ご覧のとおり、int と、WEX::Common::String の両方として取得すること。

```cpp
                int x = 0;
                String xString;
                RuntimeParameters::TryGetValue(L"x", x);
                RuntimeParameters::TryGetValue(L"x", xString);
```

詳細については、次を参照してください、 [TAEF します。ランタイム パラメーター](runtime-parameters.md)ヘルプ ページ。

### <a name="span-idparallelspanspan-idparallelspanparallel"></a><span id="parallel"></span><span id="PARALLEL"></span>/parallel

複数のプロセッサ全体には、並列でテストを実行します。 テストする必要がありますにオプトイン並列実行で 'Parallel' のメタデータでマークされています。

**te.exe test1.dll/parallel**

詳細については、次を参照してください、[並列](parallel.md)ヘルプ ページ。

### <a name="span-idpersistpictresultsspanspan-idpersistpictresultsspanspan-idpersistpictresultsspanpersistpictresults"></a><span id="persistPictResults"></span><span id="persistpictresults"></span><span id="PERSISTPICTRESULTS"></span>/persistPictResults

使用してテスト用 PICT.exe によって生成される結果をキャッシュ[PICT DataSource](pict-data-source.md)現在の実行にします。 後続のテストの実行は、同じモデル ファイルとシード ファイルに対して PICT.exe を実行している操作と同じようにキャッシュされた結果を利用しようとします。

### <a name="span-idpictspanspan-idpictspanpictltoptionnamegtltoptionvaluegt"></a><span id="pict"></span><span id="PICT"></span>/pict:&lt;OptionName&gt;=&lt;OptionValue&gt;

オプションは、使用してテストを制御する PICT.exe で呼び出されたときに、 [PICT DataSource](pict-data-source.md)します。 現在これらのオプションのいずれかを設定すると、コードに関連付けられているすべてのメタデータが上書きされます。 次のオプションが使用できます。

<span id="_Pict_Order_3"></span><span id="_pict_order_3"></span><span id="_PICT_ORDER_3"></span>/Pict:Order=3  
PICT.exe の/o コマンド オプションを使用して、値を渡すことによって、組み合わせの順序を設定します。

<span id="_Pict_ValueSeparator__"></span><span id="_pict_valueseparator__"></span><span id="_PICT_VALUESEPARATOR__"></span>/Pict:ValueSeparator=;  
PICT.exe の/d コマンド オプションを使用して、値を渡すことによって、値の区切り記号を設定します。

<span id="_Pict_AliasSeparator__"></span><span id="_pict_aliasseparator__"></span><span id="_PICT_ALIASSEPARATOR__"></span>/Pict:AliasSeparator = +  
PICT.exe の/a コマンド オプションを使用して、値を渡すことによって、エイリアスの区切り記号を設定します。

<span id="_Pict_NegativeValuePrefix__"></span><span id="_pict_negativevalueprefix__"></span><span id="_PICT_NEGATIVEVALUEPREFIX__"></span>/Pict:NegativeValuePrefix=!  
PICT.exe の/n コマンド オプションを使用して、値を渡すことによって、負の値のプレフィックスを設定します。

<span id="_pict_seedingfile_test.seed"></span><span id="_PICT_SEEDINGFILE_TEST.SEED"></span>/Pict:SeedingFile=test.seed  
PICT.exe の/e コマンド オプションを使用して、値を渡すことによってシード処理のファイルへのパスを設定します。

<span id="_Pict_Random_true"></span><span id="_pict_random_true"></span><span id="_PICT_RANDOM_TRUE"></span>/Pict:Random=true  
有効または無効 PICT 結果の乱数性能、PICT データ ソースを使用したランダム シードをログにします。

<span id="_Pict_RandomSeed_33"></span><span id="_pict_randomseed_33"></span><span id="_PICT_RANDOMSEED_33"></span>/Pict:RandomSeed=33  
PICT.exe の/r コマンド オプションを使用して、値を渡すことによって、ランダム シードを設定します。 Pict は、この設定が有効になります: ランダムな場合を除き、Pict: ランダムが明示的に false に設定します。

<span id="_Pict_CaseSensitive_true"></span><span id="_pict_casesensitive_true"></span><span id="_PICT_CASESENSITIVE_TRUE"></span>/Pict:CaseSensitive=true  
True の場合、有効に設定すると PICT.exe に/c コマンドのオプションを渡すことで大文字小文字の区別にします。

<span id="_Pict_Timeout_00_01_30"></span><span id="_pict_timeout_00_01_30"></span><span id="_PICT_TIMEOUT_00_01_30"></span>/Pict:Timeout=00:01:30  
PICT.exe が完了するまでそのプロセスを強制終了を待機する時間を設定します。 値の形式が\[日\]。1 時間\[: 分\[: 2 つ目\[します。FractionalSeconds\]\]\]します。

### <a name="span-idrunasspanspan-idrunasspanrunasltrunastypegt"></a><span id="runas"></span><span id="RUNAS"></span>/runas:&lt;RunAsType&gt;

指定された環境でテストを実行します。 参照してください、 [RunAs](runas.md)使用状況の詳細については、ドキュメント。

<span id="te.exe__.dll__runas_System"></span><span id="te.exe__.dll__runas_system"></span><span id="TE.EXE__.DLL__RUNAS_SYSTEM"></span>te.exe \*.dll/runas:System  
**解釈します。** システムとして、すべてのテストを実行します。

<span id="te.exe__.dll__runas_Elevated"></span><span id="te.exe__.dll__runas_elevated"></span><span id="TE.EXE__.DLL__RUNAS_ELEVATED"></span>te.exe \*.dll /runas:Elevated  
**解釈します。** 管理者特権でのユーザーとして、すべてのテストを実行します。

<span id="te.exe__.dll__runas_Restricted"></span><span id="te.exe__.dll__runas_restricted"></span><span id="TE.EXE__.DLL__RUNAS_RESTRICTED"></span>te.exe \*.dll /runas:Restricted  
**解釈します。** 非管理者の特権ユーザーとして、すべてのテストを実行します。

<span id="te.exe__.dll__runas_LowIL"></span><span id="te.exe__.dll__runas_lowil"></span><span id="TE.EXE__.DLL__RUNAS_LOWIL"></span>te.exe \*.dll /runas:LowIL  
**解釈します。** 低い整合性プロセスでは、すべてのテストを実行します。

### <a name="span-idrunignoredtestsspanspan-idrunignoredtestsspanspan-idrunignoredtestsspanrunignoredtests"></a><span id="runIgnoredTests"></span><span id="runignoredtests"></span><span id="RUNIGNOREDTESTS"></span>/runIgnoredTests

実行するかを示します (と共に場合[/list](#list)または[/listProperties](#listproperties)) など、すべてのテストはテスト クラスと、"true"に「無視」のメタデータ セットを持つメソッドをテストします。 既定のテスト クラスとテストによって"true"に「無視」のメタデータ セットを持つメソッドは一覧中や実行中にスキップされます。

### <a name="span-idrunonspanspan-idrunonspanrunonltmachinenamegt"></a><span id="runon"></span><span id="RUNON"></span>/runon:&lt;MachineName&gt;

指定されたコンピューターにリモートでテストを実行します。 TAEF で認証し承認、テストを実行するために必要なバイナリを展開し、元のコンソールに戻り、すべての情報を記録します。 参照してください、[クロス マシンのテストの実行](cross-machine-execution.md)使用状況の詳細については、ドキュメント。

<span id="te.exe__.dll__runon_TestMachine1"></span><span id="te.exe__.dll__runon_testmachine1"></span><span id="TE.EXE__.DLL__RUNON_TESTMACHINE1"></span>te.exe \*.dll /runon:TestMachine1  
**解釈します。**"TestMachine1"のすべてのテストをリモートで実行します。

### <a name="span-idselectspanspan-idselectspanselectltquerygt"></a><span id="select"></span><span id="SELECT"></span>/select:&lt;query&gt;

各テストを選択するときに使用される選択条件では、バイナリをテストします。 選択基準は、次の 1 つ以上で構成されます。

@\[プロパティ名\] = \[値を文字列として\]
@\[プロパティ名\] &gt; = \[値を浮動小数点または整数として\] 
@\[プロパティ名\] &gt; \[値を浮動小数点または整数として\]
@\[プロパティ名\] &lt;= \[値を浮動小数点または整数として\]
@\[プロパティ名\] &lt; \[と浮動小数点または整数値\]
-   *プロパティ値を文字列としては、単一引用符で囲んである必要があります。*
-   *使用して複合選択条件を指定する「および」,「または」、"not"(大文字と小文字は区別されません)。*
-   *プロパティの文字列値を使用してワイルドカード文字はサポート"\*「と」?"文字です。*
-   *浮動小数点と整数の値を"\*"文字は、'exists' が、部分一致では使用できませんにも使用可能性があります。* 例:**選択/:"@Priority=\*"** 有効ですが**選択/:"@Priority= 4\*"** はありません。

<span id="te.exe_test1.dll__select____Name___TestToLower__or__Owner__C2___and_not__Priority___3__"></span><span id="te.exe_test1.dll__select____name___testtolower__or__owner__c2___and_not__priority___3__"></span><span id="TE.EXE_TEST1.DLL__SELECT____NAME___TESTTOLOWER__OR__OWNER__C2___AND_NOT__PRIORITY___3__"></span>te.exe test1.dll リンク:"(@Name='\*TestToLower' または@Owner= 'C2') および not (@Priority &lt; 3)"  
**解釈します。** メソッド名が 'TestToLower' または 'C2'; の所有者を終了 test1.dll ですべてのテストを実行します。優先順位が 3 未満ではありません。

<span id="te.exe_test1.dll_test2.dll__select__Priority__"></span><span id="te.exe_test1.dll_test2.dll__select__priority__"></span><span id="TE.EXE_TEST1.DLL_TEST2.DLL__SELECT__PRIORITY__"></span>te.exe test1.dll test2.dll /select:@Priority=\*  
**解釈します。** テスト メタデータで優先順位が指定されている test1.dll と test2.dll ですべてのテストを実行します。

<span id="te.exe_test1.dll__select__Name___StringTest__"></span><span id="te.exe_test1.dll__select__name___stringtest__"></span><span id="TE.EXE_TEST1.DLL__SELECT__NAME___STRINGTEST__"></span>te.exe test1.dll /select:@Name='\*StringTest\*'  
**解釈します。** その名前空間、クラスまたはメソッド名に 'StringTest' test1.dll という語句を含むすべてのテストを実行します。

### <a name="span-idsessiontimeoutspanspan-idsessiontimeoutspanspan-idsessiontimeoutspansessiontimeoutltvaluegt"></a><span id="sessionTimeout"></span><span id="sessiontimeout"></span><span id="SESSIONTIMEOUT"></span>/sessionTimeout:&lt;value&gt;

Te.exe の実行全体のセッションのタイムアウトを設定します。 タイムアウトに達すると、テスト セッションが正常に中止され、プロセス終了コードは、タイムアウトが発生したことを示します。

**注:** タイムアウト値は、次の形式で指定する必要があります。

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]] 
```

**注:** WTT、実行されている場合、TAEF セッションがタイムアウトになる場合でも、Wtt のログ ファイルがそのまま保たれるようにするこの値を使用できます。

<span id="te.exe_test1.dll__sessionTimeout_0_0_0.5"></span><span id="te.exe_test1.dll__sessiontimeout_0_0_0.5"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_0_0.5"></span>te.exe test1.dll/sessionTimeout:0:0:0.5  
テスト全体のセッションは、.5 秒後にタイムアウトします。

<span id="te.exe_test1.dll__sessionTimeout_0_0_45"></span><span id="te.exe_test1.dll__sessiontimeout_0_0_45"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_0_45"></span>te.exe test1.dll/sessionTimeout:0:0:45  
テスト全体のセッションは 45 秒後にタイムアウトになります。

<span id="te.exe_test1.dll__sessionTimeout_0_20"></span><span id="te.exe_test1.dll__sessiontimeout_0_20"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_20"></span>te.exe test1.dll /sessionTimeout:0:20  
テスト全体のセッションが 20 分後にタイムアウトになります。

<span id="te.exe_test1.dll__sessionTimeout_5"></span><span id="te.exe_test1.dll__sessiontimeout_5"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_5"></span>te.exe test1.dll/sessionTimeout:5  
テスト全体のセッションが 5 時間後にタイムアウトになります。

<span id="te.exe_test1.dll__sessionTimeout_1.2"></span><span id="te.exe_test1.dll__sessiontimeout_1.2"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_1.2"></span>te.exe test1.dll/sessionTimeout:1.2  
テスト全体のセッションが 1 日 2 時間後にタイムアウトになります。

### <a name="span-idterminateonfirstfailurespanspan-idterminateonfirstfailurespanspan-idterminateonfirstfailurespanterminateonfirstfailure"></a><span id="terminateOnFirstFailure"></span><span id="terminateonfirstfailure"></span><span id="TERMINATEONFIRSTFAILURE"></span>/terminateOnFirstFailure

テストのテスト エラーが発生した初めての実行を終了します。 そのテストのすべての破棄操作が呼び出されますが、後続のすべてのテストが無視とマークされます。 既知の問題により、テストがテスト モードを使用するときに実行を続ける可能性があります。

**te.exe test1.dll/terminateOnFirstFailure**

### <a name="span-idtestdependenciesspanspan-idtestdependenciesspanspan-idtestdependenciesspantestdependenciesltfilesgt"></a><span id="testDependencies"></span><span id="testdependencies"></span><span id="TESTDEPENDENCIES"></span>/testDependencies:&lt;ファイル&gt;

デプロイを使用する場合に、追加のテストの依存関係を指定[マシンのテストの実行をクロス](cross-machine-execution.md)します。 完全なパスを指定しない限り、テスト ディレクトリではなく、現在のディレクトリを基準 TAEF が検索されます。

<span id="te.exe__.dll__runon_TestMachine1__TestDependencies_test_.jpg_file1.doc"></span><span id="te.exe__.dll__runon_testmachine1__testdependencies_test_.jpg_file1.doc"></span><span id="TE.EXE__.DLL__RUNON_TESTMACHINE1__TESTDEPENDENCIES_TEST_.JPG_FILE1.DOC"></span>te.exe \*.dll /runon:TestMachine1 /TestDependencies:test\*.jpg;file1.doc  
**解釈します。**"TestMachine1"でコピー、すべてのテストをリモートで実行 ' テスト\*.jpg' と 'file1.doc' 経由で任意のテストを実行する前に、リモート コンピューターにします。 各ファイルの仕様は、ワイルドカード文字を含めることができます (test.txt; テスト\*.dll など) を 1 つまたは複数のファイルと一致します。

### <a name="span-idtesttimeoutspanspan-idtesttimeoutspanspan-idtesttimeoutspantesttimeoutltvaluegt"></a><span id="testTimeout"></span><span id="testtimeout"></span><span id="TESTTIMEOUT"></span>/testTimeout:&lt;値&gt;

Te.exe の実行全体のグローバルのテストのタイムアウトを設定します。 この値には、いずれかがよりも優先[テスト タイムアウト](standard-test-metadata.md)メタデータが実行されている指定されたテストの設定されている可能性があります。

**注:** タイムアウト値は、次の形式で指定する必要があります。

```cpp
[Day.]Hour[:Minute[:Second[.FractionalSeconds]]] 
```

**注:** 組み合わせて使用する場合は無視されます[/inproc](#inproc)します。

<span id="te.exe_test1.dll__testTimeout_0_0_0.5"></span><span id="te.exe_test1.dll__testtimeout_0_0_0.5"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_0_0.5"></span>te.exe test1.dll/testTimeout:0:0:0.5  
すべてのテストとセットアップ/クリーンアップ メソッドは、.5 秒後にタイムアウトします。

<span id="te.exe_test1.dll__testTimeout_0_0_45"></span><span id="te.exe_test1.dll__testtimeout_0_0_45"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_0_45"></span>te.exe test1.dll/testTimeout:0:0:45  
すべてのテストとセットアップ/クリーンアップ メソッドは、45 秒後にタイムアウトします。

<span id="te.exe_test1.dll__testTimeout_0_20"></span><span id="te.exe_test1.dll__testtimeout_0_20"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_20"></span>te.exe test1.dll /testTimeout:0:20  
すべてのテストとセットアップ/クリーンアップ メソッドは、20 分後にタイムアウトします。

<span id="te.exe_test1.dll__testTimeout_5"></span><span id="te.exe_test1.dll__testtimeout_5"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_5"></span>te.exe test1.dll/testTimeout:5  
すべてのテストとセットアップ/クリーンアップ メソッドは 5 時間後にタイムアウトになります。

<span id="te.exe_test1.dll__testTimeout_1.2"></span><span id="te.exe_test1.dll__testtimeout_1.2"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_1.2"></span>te.exe test1.dll/testTimeout:1.2  
すべてのテストとセットアップ/クリーンアップ メソッドは、1 日 2 時間後にタイムアウトします。

### <a name="span-idunicodeoutputspanspan-idunicodeoutputspanspan-idunicodeoutputspanunicodeoutputlttruefalsegt"></a><span id="unicodeOutput"></span><span id="unicodeoutput"></span><span id="UNICODEOUTPUT"></span>/unicodeOutput:&lt;true または false&gt;

TE は、テキスト ファイルにパイプされます、ときに、既定で unicode を出力します。 1 つの例外は、既存の ANSII ファイルに追加することが要求かどうか (を使用して '&gt;&gt;')。

この動作をオーバーライドするには/unicodeOutput:false を指定することがあります。 これで、TE ANSII をファイルに常に出力します。

**te.exe test1.dll/unicodeOutput:false &gt; output.txt**

## <a name="span-idloggersettingsspanspan-idloggersettingsspanspan-idloggersettingsspanlogger-settings"></a><span id="LoggerSettings"></span><span id="loggersettings"></span><span id="LOGGERSETTINGS"></span>ロガーの設定


### <a name="span-idappendwttloggingspanspan-idappendwttloggingspanspan-idappendwttloggingspanappendwttlogging"></a><span id="appendWttLogging"></span><span id="appendwttlogging"></span><span id="APPENDWTTLOGGING"></span>/appendWttLogging

WTT ログ記録が有効な場合は、上書きするのではなく、ログ ファイルに追加します。 組み合わせて使用する必要があります[/enableWttLogging](#enablewttlogging)します。

<span id="te.exe_test1.dll__enableWttLogging__appendWttLogging"></span><span id="te.exe_test1.dll__enablewttlogging__appendwttlogging"></span><span id="TE.EXE_TEST1.DLL__ENABLEWTTLOGGING__APPENDWTTLOGGING"></span>te.exe test1.dll/enableWttLogging/appendWttLogging  
作成、またはという名前のログ ファイルに追加されます*TE.wtl*テストの実行が完了します。

### <a name="span-idenablewttloggingspanspan-idenablewttloggingspanspan-idenablewttloggingspanenablewttlogging"></a><span id="enableWttLogging"></span><span id="enablewttlogging"></span><span id="ENABLEWTTLOGGING"></span>/enableWttLogging

WTT; のログ記録を有効にします。Wttlog.dll は、パスで使用可能なである必要があります。

<span id="te.exe_test1.dll__enableWttLogging"></span><span id="te.exe_test1.dll__enablewttlogging"></span><span id="TE.EXE_TEST1.DLL__ENABLEWTTLOGGING"></span>te.exe test1.dll/enableWttLogging  
という名前のログ ファイルが生成されます*TE.wtl*テストの実行が完了します。

### <a name="span-iddefaultappdomainspanspan-iddefaultappdomainspanspan-iddefaultappdomainspandefaultappdomain"></a><span id="defaultAppDomain"></span><span id="defaultappdomain"></span><span id="DEFAULTAPPDOMAIN"></span>/defaultAppDomain

既定のアプリケーション ドメインでは、管理対象のテストを実行します。

<span id="te.exe_managed.test1.dll__defaultAppDomain"></span><span id="te.exe_managed.test1.dll__defaultappdomain"></span><span id="TE.EXE_MANAGED.TEST1.DLL__DEFAULTAPPDOMAIN"></span>te.exe managed.test1.dll/defaultAppDomain  

### <a name="span-iddisableconsoleloggingspanspan-iddisableconsoleloggingspanspan-iddisableconsoleloggingspandisableconsolelogging"></a><span id="disableConsoleLogging"></span><span id="disableconsolelogging"></span><span id="DISABLECONSOLELOGGING"></span>/disableConsoleLogging

コンソール ログ出力を無効にします。組み合わせて使用する必要があります[/enableWttLogging](#enablewttlogging)します。

**te.exe test1.dll/disableConsoleLogging/enableWttLogging**

### <a name="span-idlogfilespanspan-idlogfilespanspan-idlogfilespanlogfileltnamegt"></a><span id="logFile"></span><span id="logfile"></span><span id="LOGFILE"></span>/logFile:&lt;name&gt;

Wtt ログ ファイルとして使用する名前を指定します。組み合わせて使用する必要があります[/enableWttLogging](#enablewttlogging)します。

<span id="te.exe_test1.dll__logFile_myCustomLogFile.xml__enableWttLogging"></span><span id="te.exe_test1.dll__logfile_mycustomlogfile.xml__enablewttlogging"></span><span id="TE.EXE_TEST1.DLL__LOGFILE_MYCUSTOMLOGFILE.XML__ENABLEWTTLOGGING"></span>te.exe test1.dll /logFile:myCustomLogFile.xml /enableWttLogging  
という名前のログ ファイルが生成されます*myCustomeLogFile.xml*テストの実行が完了します。

### <a name="span-idlogoutputspanspan-idlogoutputspanspan-idlogoutputspanlogoutputltmodegt"></a><span id="logOutput"></span><span id="logoutput"></span><span id="LOGOUTPUT"></span>/logOutput:&lt;mode&gt;

ロガーの出力レベルを設定します。 有効な値は次のとおりです。

-   *高*:すべてのトレースの横にあるタイムスタンプの印刷などの何らかの他のコンソール出力を有効にします。
-   *低*:唯一のコア イベント (開始、終了グループなど) とエラーを出力します。 ログ ファイルには、低い優先順位の詳細の前に、エラーのコンテキストを提供するすべてのエラーが含まれます。
-   *LowWithConsoleBuffering*:同じ*低*、ログ ファイルとコンソールの出力エラーのコンテキストが含まれています。
-   *最も低い*:同じ*低*、コンソール出力には、エラーのみ、テストの失敗、および実行の概要が含まれています。

### <a name="span-idversionspanspan-idversionspanversion"></a><span id="version"></span><span id="VERSION"></span>/version

詳細なバージョン情報を出力します。

### <a name="span-idwttdevicestringspanspan-idwttdevicestringspanspan-idwttdevicestringspanwttdevicestringltvaluegt"></a><span id="wttDeviceString"></span><span id="wttdevicestring"></span><span id="WTTDEVICESTRING"></span>/wttDeviceString:&lt;value&gt;

WexLogger WttLogger を初期化するときに使用する WttDeviceString を完全に上書きします。

**te.exe test1.dll /wttDeviceString:$Console**

### <a name="span-idwttdevicestringsuffixspanspan-idwttdevicestringsuffixspanspan-idwttdevicestringsuffixspanwttdevicestringsuffixltvaluegt"></a><span id="wttDeviceStringSuffix"></span><span id="wttdevicestringsuffix"></span><span id="WTTDEVICESTRINGSUFFIX"></span>/wttDeviceStringSuffix:&lt;value&gt;

既定 WttDeviceString WexLogger WttLogger を初期化するときに使用するには、指定した値を追加します。 場合は無視されます[wttDeviceString](#wttdevicestringsuffix)も指定します。

**te.exe test1.dll /wttDeviceStringSuffix:$Console**

## <a name="span-iddebugsettingsspanspan-iddebugsettingsspanspan-iddebugsettingsspandebug-settings"></a><span id="DebugSettings"></span><span id="debugsettings"></span><span id="DEBUGSETTINGS"></span>デバッグの設定


### <a name="span-idbreakoncreatespanspan-idbreakoncreatespanspan-idbreakoncreatespanbreakoncreate"></a><span id="breakOnCreate"></span><span id="breakoncreate"></span><span id="BREAKONCREATE"></span>/breakOnCreate

各テスト クラスをインスタンス化する前にデバッガーを中断します。

**te.exe test1.dll/breakOnCreate**

### <a name="span-idbreakonerrorspanspan-idbreakonerrorspanspan-idbreakonerrorspanbreakonerror"></a><span id="breakOnError"></span><span id="breakonerror"></span><span id="BREAKONERROR"></span>/breakOnError

エラーまたはテストの失敗が記録された場合は、デバッガーを中断します。

**te.exe test1.dll/breakOnError**

### <a name="span-idbreakoninvokespanspan-idbreakoninvokespanspan-idbreakoninvokespanbreakoninvoke"></a><span id="breakOnInvoke"></span><span id="breakoninvoke"></span><span id="BREAKONINVOKE"></span>/breakOnInvoke

各テスト メソッドを呼び出す前にデバッガーを中断します。

**te.exe test1.dll/breakOnInvoke**

### <a name="span-iddisabletimeoutsspanspan-iddisabletimeoutsspanspan-iddisabletimeoutsspandisabletimeouts"></a><span id="disableTimeouts"></span><span id="disabletimeouts"></span><span id="DISABLETIMEOUTS"></span>/disableTimeouts

実行中には、すべてのタイムアウトを無効にします。 これはできるデバッグ時は、デバッグ中のプログラム側 TAEF が待機しているときにタイムアウトを防ぐために役立つこと。

**te.exe test1.dll/disableTimeouts**

### <a name="span-idminidumponerrorspanspan-idminidumponerrorspanspan-idminidumponerrorspanminidumponerror"></a><span id="miniDumpOnError"></span><span id="minidumponerror"></span><span id="MINIDUMPONERROR"></span>/miniDumpOnError

テストのエラーまたは障害が発生する場合は、ミニ ダンプをログ記録を受け取り。

**te.exe test1.dll/miniDumpOnError**

### <a name="span-idminidumponcrashspanspan-idminidumponcrashspanspan-idminidumponcrashspanminidumponcrash"></a><span id="miniDumpOnCrash"></span><span id="minidumponcrash"></span><span id="MINIDUMPONCRASH"></span>/miniDumpOnCrash

テスト クラッシュが発生した場合に、ミニ ダンプをログ記録を受け取り。

**te.exe test1.dll/miniDumpOnCrash**

### <a name="span-idrebootstatefilespanspan-idrebootstatefilespanspan-idrebootstatefilespanrebootstatefile"></a><span id="rebootStateFile"></span><span id="rebootstatefile"></span><span id="REBOOTSTATEFILE"></span>/rebootStateFile

実行を明示的に有効[再起動](reboot.md)テストします。

**te.exe test1.dll /rebootStateFile:myFile.xml**

### <a name="span-idreportloadingissuespanspan-idreportloadingissuespanspan-idreportloadingissuespanreportloadingissue"></a><span id="reportLoadingIssue"></span><span id="reportloadingissue"></span><span id="REPORTLOADINGISSUE"></span>/reportLoadingIssue

TAEF がテスト dll の読み込みに失敗したときに、エラーの説明ダイアログが表示されます。 ネイティブ テスト dll の読み込みに関する問題の調査のためにのみ使用する必要があります。

**te.exe test1.dll/reportLoadingIssue**

### <a name="span-idscreencaptureonerrorspanspan-idscreencaptureonerrorspanspan-idscreencaptureonerrorspanscreencaptureonerror"></a><span id="screenCaptureOnError"></span><span id="screencaptureonerror"></span><span id="SCREENCAPTUREONERROR"></span>/screenCaptureOnError

テストのエラーや障害が発生した場合、画面キャプチャのログに記録します。

**te.exe test1.dll/screenCaptureOnError**

### <a name="span-idstackframecountspanspan-idstackframecountspanspan-idstackframecountspanstackframecountltvaluegt"></a><span id="stackFrameCount"></span><span id="stackframecount"></span><span id="STACKFRAMECOUNT"></span>/stackFrameCount:&lt;value&gt;

呼び出し履歴を取得するときに表示するスタック フレームの数を指定します。 既定値には 50 です。

**te.exe test1.dll/stackFrameCount:100**

### <a name="span-idstacktraceonerrorspanspan-idstacktraceonerrorspanspan-idstacktraceonerrorspanstacktraceonerror"></a><span id="stackTraceOnError"></span><span id="stacktraceonerror"></span><span id="STACKTRACEONERROR"></span>/stackTraceOnError

テスト エラーや障害が発生した場合は、スタック トレースをログ記録を受け取り。

**te.exe test1.dll/stackTraceOnError**

## <a name="span-idtestmodesspanspan-idtestmodesspanspan-idtestmodesspantest-modes"></a><span id="TestModes"></span><span id="testmodes"></span><span id="TESTMODES"></span>テスト モード


### <a name="span-idlooptestmodespanspan-idlooptestmodespanspan-idlooptestmodespantestmodeloop"></a><span id="loopTestMode"></span><span id="looptestmode"></span><span id="LOOPTESTMODE"></span>/testmode:Loop

により、2 つの変数を使用して実行を制御する*ループ*と*LoopTest*します。

-   *ループ*:コントロール全体の実行回数が実行されます。 既定の 1 です。
-   *LoopTest*:個々 のテストの実行回数を制御します。 既定の 10 です。

<span id="te.exe_test1.dll__testmode_Loop"></span><span id="te.exe_test1.dll__testmode_loop"></span><span id="TE.EXE_TEST1.DLL__TESTMODE_LOOP"></span>te.exe test1.dll /testmode:Loop  
**解釈します。** Test1.dll 10 回ですべてのテストを実行 (既定値の*LoopTest*)。 全体の実行が 1 回実行 (既定値の*ループ*)。

<span id="te.exe_test1.dll_test2.dll__testmode_Loop__Loop_3__LoopTest_1"></span><span id="te.exe_test1.dll_test2.dll__testmode_loop__loop_3__looptest_1"></span><span id="TE.EXE_TEST1.DLL_TEST2.DLL__TESTMODE_LOOP__LOOP_3__LOOPTEST_1"></span>te.exe test1.dll test2.dll /testmode:Loop /Loop:3 /LoopTest:1  
**解釈します。** 1 回 test1.dll と test2.dll ですべてのテストを実行 (によって決まります*LoopTest*)。 全体の実行 (test1.dll と test2.dll ですべての結合のテスト) を 3 回 - によって決定される実行*ループ*します。

### <a name="span-idstressspanspan-idstressspantestmodestress"></a><span id="stress"></span><span id="STRESS"></span>/testmode:Stress

'Stress' テスト モードで TAEF はまたはテストを実行、無期限に Ctrl キーを押しながら C キーを入力するまで、WM まで\_閉じるメッセージ TAEF の非表示のウィンドウに送信されます。 組み合わせて/testmode:stress を実行する必要があります[/inproc](#inproc)します。

**te.exe test1.dll /testmode:Stress /inproc**

詳細な情報とその他のパラメーターがこのモードでサポートされているドキュメントを参照してください。[ここ](test-modes.md)します。










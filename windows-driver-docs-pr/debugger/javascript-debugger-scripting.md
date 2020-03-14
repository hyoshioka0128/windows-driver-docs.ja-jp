---
title: JavaScript デバッガーのスクリプト
description: このトピックでは、JavaScript を使用して、デバッガーオブジェクトを理解し、デバッガーの機能を拡張およびカスタマイズするスクリプトを作成する方法について説明します。
ms.assetid: 3442E2C4-4054-4698-B7FB-8FE19D26C171
ms.date: 04/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: b01aed239dabef52d3fcd3a37c1feb56b1f5920b
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242785"
---
# <a name="javascript-debugger-scripting"></a>JavaScript デバッガーのスクリプト


このトピックでは、JavaScript を使用して、デバッガーオブジェクトを理解し、デバッガーの機能を拡張およびカスタマイズするスクリプトを作成する方法について説明します。

## <a name="span-idoverview_of_javascript_debugger_scripting_spanspan-idoverview_of_javascript_debugger_scripting_spanspan-idoverview_of_javascript_debugger_scripting_spanoverview-of-javascript-debugger-scripting"></a><span id="Overview_of_JavaScript_Debugger_Scripting_"></span><span id="overview_of_javascript_debugger_scripting_"></span><span id="OVERVIEW_OF_JAVASCRIPT_DEBUGGER_SCRIPTING_"></span>JavaScript デバッガースクリプトの概要


スクリプトプロバイダーは、スクリプト言語をデバッガーの内部オブジェクトモデルにブリッジします。 JavaScript デバッガースクリプトプロバイダーは、デバッガーで JavaScript を使用できるようにします。

. Scriptload コマンドを使用して JavaScript が読み込まれると、スクリプトのルートコードが実行され、スクリプト内に存在する名前がデバッガーのルート名前空間 (dx デバッガー) に格納され、スクリプトはアンロードされるまでメモリに常駐します。オブジェクトへのすべての参照が解放されます。 このスクリプトでは、デバッガーの式エバリュエーターに新しい関数を提供したり、デバッガーのオブジェクトモデルを変更したりできます。また、NatVis ビジュアライザーとほとんど同じようにビジュアライザーとして機能させることもできます。

このトピックでは、JavaScript デバッガースクリプトで実行できるいくつかの操作について説明します。

これらの2つのトピックでは、デバッガーでの JavaScript の操作に関する追加情報を提供します。

[JavaScript デバッガーのサンプルスクリプト](javascript-debugger-example-scripts.md)

[JavaScript 拡張機能のネイティブオブジェクト](native-objects-in-javascript-extensions.md)


## <a name="javascript-scripting-video"></a>JavaScript スクリプトビデオ

[デフラグツール #170](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-170-Debugger-JavaScript-Scripting) -Andy と Bill は、デバッガーでの JavaScript の拡張機能とスクリプト機能を示しています。


## <a name="span-idproviderspanspan-idproviderspanspan-idproviderspanthe-debugger-javascript-provider"></a><span id="Provider"></span><span id="provider"></span><span id="PROVIDER"></span>デバッガー JavaScript プロバイダー

デバッガーに含まれる JavaScript プロバイダーは、最新の ECMAScript6 オブジェクトとクラスの機能強化を最大限に活用します。 詳細については、「 [ECMAScript 6-新機能: 概要 & 比較](https://es6-features.org/)」を参照してください。

**JsProvider**

JsProvider は、JavaScript デバッガーのスクリプト作成をサポートするために読み込まれる JavaScript プロバイダーです。

**必要性**

JavaScript デバッガーのスクリプト作成は、サポートされているすべてのバージョンの Windows で動作するように設計されています。

## <a name="span-idloading_the_javascript_scripting_providerspanspan-idloading_the_javascript_scripting_providerspanspan-idloading_the_javascript_scripting_providerspanloading-the-javascript-scripting-provider"></a><span id="Loading_the_JavaScript_Scripting_Provider"></span><span id="loading_the_javascript_scripting_provider"></span><span id="LOADING_THE_JAVASCRIPT_SCRIPTING_PROVIDER"></span>JavaScript スクリプトプロバイダーを読み込んでいます


スクリプトコマンドを使用する前に、スクリプトプロバイダーを読み込むには、 [**load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用する必要があります。 JavaScript プロバイダーを読み込むには、次のコマンドを使用します。

```dbgcmd
0:000> .load jsprovider.dll
```

[Scriptproviders] コマンドを使用して、JavaScript プロバイダーが読み込まれていることを確認します。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

## <a name="span-idcommandsspanspan-idcommandsspanspan-idcommandsspanjavascript-scripting-meta-commands"></a><span id="Commands"></span><span id="commands"></span><span id="COMMANDS"></span>JavaScript スクリプト作成メタコマンド


JavaScript デバッガースクリプトを操作するには、次のコマンドを使用できます。

-   [**scriptproviders (List スクリプトプロバイダー)** ](-scriptproviders--list-script-providers-.md)
-   [**scriptload (スクリプトの読み込み)** ](-scriptload--load-script-.md)
-   [**scriptunload (アンロードスクリプト)** ](-scriptunload--unload-script-.md)
-   [**scriptrun (スクリプトの実行)** ](-scriptrun--run-script-.md)
-   [**scriptlist (読み込まれたスクリプトの一覧表示)** ](-scriptlist--list-loaded-scripts-.md)

**必要性**

スクリプトコマンドを使用する前に、スクリプトプロバイダーを読み込むには、 [**load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用する必要があります。 JavaScript プロバイダーを読み込むには、次のコマンドを使用します。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idscriptproviders__list_script_providers_spanspan-idscriptproviders__list_script_providers_spanscriptproviders-list-script-providers"></a><span id=".scriptproviders__list_script_providers_"></span><span id=".SCRIPTPROVIDERS__LIST_SCRIPT_PROVIDERS_"></span>scriptproviders (List スクリプトプロバイダー)


Scriptproviders コマンドは、現在デバッガーによって認識されているすべてのスクリプト言語と、それが登録されている拡張機能の一覧を表示します。

次の例では、JavaScript プロバイダーと NatVis プロバイダーが読み込まれています。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

"" で終わるすべてのファイル。NatVis "は NatVis スクリプトとして認識され、" .js "で終わるすべてのファイルは JavaScript スクリプトとして認識されます。 Scriptload コマンドを使用して、どちらの種類のスクリプトでも読み込むことができます。

詳細については、「 [ **scriptproviders (List スクリプトプロバイダー)** 」を参照してください。](-scriptproviders--list-script-providers-.md)

## <a name="span-idscriptload__load_script_spanspan-idscriptload__load_script_spanscriptload-load-script"></a><span id=".scriptload__load_script_"></span><span id=".SCRIPTLOAD__LOAD_SCRIPT_"></span>scriptload (スクリプトの読み込み)


Scriptload コマンドは、スクリプトを読み込み、スクリプトと*initializeScript*関数のルートコードを実行します。 スクリプトの初回読み込み時および実行時にエラーが発生した場合、エラーはコンソールに表示されます。 次のコマンドは、TestScript の成功した読み込みを示しています。

```dbgcmd
0:000> .scriptload C:\WinDbg\Scripts\TestScript.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\TestScript.js'
```

スクリプトによって行われたオブジェクトモデルの操作は、スクリプトがアンロードされるか、別のコンテンツで再び実行されるまで、そのまま維持されます。

詳細については、「 [ **Scriptload (スクリプトの読み込み)** 」を参照してください。](-scriptload--load-script-.md)

## <a name="span-idscriptrunspanscriptrun"></a><span id=".SCRIPTRUN"></span>. scriptrun


Scriptrun コマンドは、スクリプトを読み込んで、スクリプトのルートコードを実行します。 *initializeScript*と*invokeScript*関数 スクリプトの初回読み込み時および実行時にエラーが発生した場合、エラーはコンソールに表示されます。

```dbgcmd
0:000> .scriptrun C:\WinDbg\Scripts\helloWorld.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\helloWorld.js'
Hello World!  We are in JavaScript!
```

スクリプトによって行われたデバッガーオブジェクトモデルの操作は、スクリプトがアンロードされるか、別のコンテンツで再び実行されるまで、そのまま維持されます。

詳細については、「[**スクリプトを実行**](-scriptrun--run-script-.md)する」を参照してください。

## <a name="span-idscriptunload__unload_script_spanspan-idscriptunload__unload_script_spanscriptunload-unload-script"></a><span id=".scriptunload__unload_script_"></span><span id=".SCRIPTUNLOAD__UNLOAD_SCRIPT_"></span>scriptunload (アンロードスクリプト)


Scriptunload コマンドは、読み込まれたスクリプトをアンロードし、 *uninitializeScript*関数を呼び出します。 スクリプトをアンロードするには、次のコマンド構文を使用します。

```dbgcmd
0:000:x86> .scriptunload C:\WinDbg\Scripts\TestScript.js
JavaScript script unloaded from 'C:\WinDbg\Scripts\TestScript.js'
```

詳細については、「 [**scriptunload (アンロードスクリプト)** ](-scriptunload--unload-script-.md)」を参照してください。

## <a name="span-idscriptlist__list_loaded_scripts_spanspan-idscriptlist__list_loaded_scripts_spanscriptlist-list-loaded-scripts"></a><span id=".scriptlist__list_loaded_scripts_"></span><span id=".SCRIPTLIST__LIST_LOADED_SCRIPTS_"></span>scriptlist (読み込まれたスクリプトの一覧表示)


Scriptlist コマンドまたは scriptrun コマンドを使用して読み込まれたすべてのスクリプトが、scriptlist コマンドによって一覧表示されます。 Scriptload を使用して TestScript が正常に読み込まれた場合、scriptload コマンドは読み込まれたスクリプトの名前を表示します。

```dbgcmd
0:000> .scriptlist
Command Loaded Scripts:
    JavaScript script from 'C:\WinDbg\Scripts\TestScript.js'
```

詳細については、「 [**scriptlist」 (読み込んだスクリプトの一覧)** ](-scriptlist--list-loaded-scripts-.md)を参照してください。

## <a name="span-idstartedspanspan-idstartedspanspan-idstartedspanget-started-with-javascript-debugger-scripting"></a><span id="Started"></span><span id="started"></span><span id="STARTED"></span>JavaScript デバッガーのスクリプト作成の概要


### <a name="span-idhelloworld_example_scriptspanspan-idhelloworld_example_scriptspanspan-idhelloworld_example_scriptspanhelloworld-example-script"></a><span id="HelloWorld_Example_Script"></span><span id="helloworld_example_script"></span><span id="HELLOWORLD_EXAMPLE_SCRIPT"></span>HelloWorld スクリプトの例

このセクションでは、Hello World 出力する単純な JavaScript デバッガースクリプトを作成して実行する方法について説明します。

```dbgcmd
// WinDbg JavaScript sample
// Prints Hello World
function initializeScript()
{
    host.diagnostics.debugLog("***> Hello World! \n");
}
```

メモ帳などのテキストエディターを使用して、前に示した JavaScript コードを含む HelloWorld という名前のテキストファイルを作成し*ます*。

[**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load jsprovider.dll
```

スクリプトを読み込んで実行するには、scriptload コマンドを使用します。 関数名*initializeScript*を使用したので、スクリプトが読み込まれるときに関数内のコードが実行されます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\HelloWorld.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\HelloWorld.js'
***> Hello World! 
```

スクリプトが読み込まれると、デバッガーで追加の機能を使用できるようになります。 [**Dx (Display NatVis Expression)** ](dx--display-visualizer-variables-.md)コマンドを使用して、スクリプトが現在常駐していることを確認するための*スクリプト*を表示します。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    HelloWorld 
```

次の例では、名前付き関数を追加して呼び出します。

### <a name="span-idadding_two_values_example_scriptspanspan-idadding_two_values_example_scriptspanspan-idadding_two_values_example_scriptspanadding-two-values-example-script"></a><span id="Adding_Two_Values_Example_Script"></span><span id="adding_two_values_example_script"></span><span id="ADDING_TWO_VALUES_EXAMPLE_SCRIPT"></span>2つの値の追加スクリプトの例

このセクションでは、を追加する単純な JavaScript デバッガースクリプトを作成して実行し、2つの数値を加算する方法について説明します。

この単純なスクリプトは、1つの関数である値を追加します。

```dbgcmd
// WinDbg JavaScript sample
// Adds two functions
function addTwoValues(a, b)
 {
     return a + b;
 }
```

メモ帳などのテキストエディターを使用して、 *Firstsamplefunction .js*という名前のテキストファイルを作成します。

[**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load jsprovider.dll
```

Scriptload コマンドを使用してスクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

スクリプトが読み込まれると、デバッガーで追加の機能を使用できるようになります。 [**Dx (Display NatVis Expression)** ](dx--display-visualizer-variables-.md)コマンドを使用して、スクリプトが現在常駐していることを確認するための*スクリプト*を表示します。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    FirstSampleFunction    
```

*Firstsamplefunction*をクリックすると、どのような機能が提供されるかを確認できます。

```dbgcmd
0:000> dx -r1 -v Debugger.State.Scripts.FirstSampleFunction.Contents
Debugger.State.Scripts.FirstSampleFunction.Contents                 : [object Object]
    host             : [object Object]
    addTwoValues    
 ... 
```

スクリプトを操作しやすくするには、dx コマンドを使用してスクリプトの内容を保持する変数をデバッガーに割り当てます。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.FirstSampleFunction.Contents
```

Dx 式エバリュエーターを使用して、Addvalues 関数を呼び出します。

```dbgcmd
0:000> dx @$myScript.addTwoValues(10, 41),d
@$myScript.addTwoValues(10, 41),d : 51
```

*@ $ScriptContents*組み込みエイリアスを使用して、スクリプトを操作することもできます。 *@ $ScriptContents*エイリアスは、すべてのをマージします。読み込まれたすべてのスクリプトの内容。

```dbgcmd
0:001> dx @$scriptContents.addTwoValues(10, 40),d
@$scriptContents.addTwoValues(10, 40),d : 50
```

スクリプトの操作が完了したら、scriptunload コマンドを使用してスクリプトをアンロードします。

```dbgcmd
0:000> .scriptunload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully unloaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

### <a name="span-idautomatespanspan-idautomatespanspan-idautomatespandebugger-command-automation"></a><span id="Automate"></span><span id="automate"></span><span id="AUTOMATE"></span>デバッガーコマンドの自動化

ここでは、 [**u (Unassemble)** ](u--unassemble-.md)コマンドの送信を自動化する単純な JavaScript デバッガースクリプトを作成して実行する方法について説明します。 このサンプルでは、ループ内でコマンドの出力を収集して表示する方法も示しています。

このスクリプトは、単一の関数 RunCommands () を提供します。

```javascript
// WinDbg JavaScript sample
// Shows how to call a debugger command and display results
"use strict";

function RunCommands()
{
var ctl = host.namespace.Debugger.Utility.Control;   
var output = ctl.ExecuteCommand("u");
host.diagnostics.debugLog("***> Displaying command output \n");

for (var line of output)
   {
   host.diagnostics.debugLog("  ", line, "\n");
   }

host.diagnostics.debugLog("***> Exiting RunCommands Function \n");

}
```

メモ帳などのテキストエディターを使用して、Runcommands という名前のテキストファイルを作成し*ます。*

[**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load jsprovider.dll
```

Scriptload コマンドを使用して、RunCommands スクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\RunCommands.js 
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\RunCommands.js'
```

スクリプトが読み込まれると、デバッガーで追加の機能を使用できるようになります。 [**Dx (Display NatVis Expression)** ](dx--display-visualizer-variables-.md)コマンドを使用して、スクリプトが現在常駐していることを確認するために*Debugger. runcommands*を表示します。

```dbgcmd
0:000>dx -r3 Debugger.State.Scripts.RunCommands
Debugger.State.Scripts.RunCommands                
    Contents         : [object Object]
        host             : [object Object]
            diagnostics      : [object Object]
            namespace       
            currentSession   : Live user mode: <Local>
            currentProcess   : notepad.exe
            currentThread    : ntdll!DbgUiRemoteBreakin (00007ffd`87f2f440) 
            memory           : [object Object]
```

RunCommands スクリプトで RunCommands 関数を呼び出すには、dx コマンドを使用します。

```dbgcmd
0:000> dx Debugger.State.Scripts.RunCommands.Contents.RunCommands()
  ***> Displaying command output
  ntdll!ExpInterlockedPopEntrySListEnd+0x17 [d:\rs1\minkernel\ntos\rtl\amd64\slist.asm @ 196]:
  00007ffd`87f06e67 cc              int     3
  00007ffd`87f06e68 cc              int     3
  00007ffd`87f06e69 0f1f8000000000  nop     dword ptr [rax]
  ntdll!RtlpInterlockedPushEntrySList [d:\rs1\minkernel\ntos\rtl\amd64\slist.asm @ 229]:
  00007ffd`87f06e70 0f0d09          prefetchw [rcx]
  00007ffd`87f06e73 53              push    rbx
  00007ffd`87f06e74 4c8bd1          mov     r10,rcx
  00007ffd`87f06e77 488bca          mov     rcx,rdx
  00007ffd`87f06e7a 4c8bda          mov     r11,rdx
***> Exiting RunCommands Function
```

## <a name="span-idspecial_javascript_debugger_functionsspanspan-idspecial_javascript_debugger_functionsspanspan-idspecial_javascript_debugger_functionsspanspecial-javascript-debugger-functions"></a><span id="Special_JavaScript_Debugger_Functions"></span><span id="special_javascript_debugger_functions"></span><span id="SPECIAL_JAVASCRIPT_DEBUGGER_FUNCTIONS"></span>特別な JavaScript デバッガー関数


JavaScript スクリプトには、スクリプトプロバイダー自体によって呼び出されるいくつかの特殊な関数があります。

### <a name="span-idinitializescriptspanspan-idinitializescriptspanspan-idinitializescriptspaninitializescript"></a><span id="initializeScript"></span><span id="initializescript"></span><span id="INITIALIZESCRIPT"></span>initializeScript

JavaScript スクリプトが読み込まれて実行されると、スクリプト内の変数、関数、およびその他のオブジェクトがデバッガーのオブジェクトモデルに影響を与える前に、一連の手順を実行します。

-   スクリプトはメモリに読み込まれ、解析されます。
-   スクリプト内のルートコードが実行されます。
-   スクリプトに initializeScript というメソッドが含まれている場合、そのメソッドが呼び出されます。
-   InitializeScript からの戻り値は、デバッガーのオブジェクトモデルを自動的に変更する方法を決定するために使用されます。
-   スクリプト内の名前は、デバッガーの名前空間に対してブリッジされます。

前述のように、initializeScript は、スクリプトのルートコードが実行された直後に呼び出されます。 そのジョブは、デバッガーのオブジェクトモデルを変更する方法を示す登録オブジェクトの JavaScript 配列をプロバイダーに返すことです。

```javascript
function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> initializeScript was called\n");
}
```

### <a name="span-idinvokescriptspanspan-idinvokescriptspanspan-idinvokescriptspaninvokescript"></a><span id="invokeScript"></span><span id="invokescript"></span><span id="INVOKESCRIPT"></span>invokeScript

InvokeScript メソッドは、プライマリスクリプトメソッドであり、scriptload と scriptrun が実行されるときに呼び出されます。

```javascript
function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> invokeScript was called\n");
}
```

### <a name="span-iduninitializescriptspanspan-iduninitializescriptspanspan-iduninitializescriptspanuninitializescript"></a><span id="uninitializeScript"></span><span id="uninitializescript"></span><span id="UNINITIALIZESCRIPT"></span>uninitializeScript

UninitializeScript メソッドは、initializeScript とは逆の動作です。 スクリプトのリンクが解除され、アンロードの準備が整ったときに呼び出されます。 そのジョブは、スクリプトが実行中に強制的に作成したオブジェクトモデルに対する変更を元に戻したり、スクリプトによってキャッシュされたオブジェクトを破棄したりすることです。

スクリプトによってオブジェクトモデルに対する命令型の操作が行われない場合、または結果がキャッシュされない場合は、uninitializeScript メソッドを使用する必要はありません。 InitializeScript の戻り値によって示されたとおりに実行されたオブジェクトモデルに対する変更は、プロバイダーによって自動的に元に戻されます。 このような変更には、明示的な uninitializeScript メソッドは必要ありません。

```javascript
function uninitializeScript()
{
    // Add code here that you want to run every time the script is unloaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> uninitialize was called\n");
}
```

## <a name="span-idsummary_of_functions_called_by_script_commandsspanspan-idsummary_of_functions_called_by_script_commandsspanspan-idsummary_of_functions_called_by_script_commandsspansummary-of-functions-called-by-script-commands"></a><span id="Summary_of_Functions_Called_by_Script_Commands"></span><span id="summary_of_functions_called_by_script_commands"></span><span id="SUMMARY_OF_FUNCTIONS_CALLED_BY_SCRIPT_COMMANDS"></span>スクリプトコマンドによって呼び出される関数の概要


次の表は、スクリプトコマンドによって呼び出される関数をまとめたものです。

||[scriptload](-scriptload--load-script-.md)|[scriptrun (スクリプトの実行)](-scriptrun--run-script-.md)|[scriptunload (アンロードスクリプト)](-scriptunload--unload-script-.md)|
|--- |--- |--- |--- |
|root|○|○| | |
|initializeScript|○|○| | |
|invokeScript       | |○| |
|uninitializeScript | ||○|


このサンプルコードを使用して、スクリプトの読み込み、実行、およびアンロードのたびに各関数が呼び出されるタイミングを確認します。

```javascript
// Root of Script
host.diagnostics.debugLog("***>; Code at the very top (root) of the script is always run \n");


function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; initializeScript was called \n");
}

function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; invokeScript was called \n");
}


function uninitializeScript()
{
    // Add code here that you want to run every time the script is unloaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; uninitialize was called\n");
}


function main()
{
    // main is just another function name in JavaScript
    // main is not called by .scriptload or .scriptrun  
    host.diagnostics.debugLog("***>; main was called \n");
}
```

## <a name="span-idvisualizerspanspan-idvisualizerspanspan-idvisualizerspancreating-a-debugger-visualizer-in-javascript"></a><span id="Visualizer"></span><span id="visualizer"></span><span id="VISUALIZER"></span>JavaScript でのデバッガービジュアライザーの作成


カスタムビジュアル化ファイルを使用すると、データの関係とコンテンツをより正確に反映した視覚化構造でデータをグループ化し、整理することができます。 JavaScript デバッガー拡張機能を使用して、NatVis と非常によく似た方法で動作するデバッガービジュアライザーを作成できます。 これは、特定のデータ型のビジュアライザーとして機能する JavaScript プロトタイプオブジェクト (または ES6 クラス) を作成することによって実現されます。 NatVis とデバッガーの詳細については、「 [**dx (Display NatVis Expression)** ](dx--display-visualizer-variables-.md)」を参照してください。

**クラスの例-Simple1DArray**

1次元配列を表すC++クラスの例を考えてみましょう。 このクラスには、2つのメンバー (m\_size が配列の全体のサイズ) と m\_pValues があります。これは、m\_size フィールドと同じメモリ内の int の数を指すポインターです。

```cpp
class Simple1DArray
{
private:

    ULONG64 m_size;
    int *m_pValues;
};
```

Dx コマンドを使用して、既定のデータ構造の表示を確認できます。

```dbgcmd
0:000> dx g_array1D
g_array1D                 [Type: Simple1DArray]
    [+0x000] m_size           : 0x5 [Type: unsigned __int64]
    [+0x008] m_pValues        : 0x8be32449e0 : 0 [Type: int *]
```

**JavaScript ビジュアライザー**

この型を視覚化するには、デバッガーで表示するすべてのフィールドとプロパティを含むプロトタイプ (または ES6) クラスを作成する必要があります。 また、initializeScript メソッドから、指定された型のビジュアライザーとしてプロトタイプをリンクするように JavaScript プロバイダーに指示するオブジェクトを返す必要もあります。

```javascript
function initializeScript()
{
    //
    // Define a visualizer class for the object.
    //
    class myVisualizer
    {
        //
        // Create an ES6 generator function which yields back all the values in the array.
        //
        *[Symbol.iterator]()
        {
            var size = this.m_size;
            var ptr = this.m_pValues;
            for (var i = 0; i < size; ++i)
            {
                yield ptr.dereference();

                //
                // Note that the .add(1) method here is effectively doing pointer arithmetic on
                // the underlying pointer.  It is moving forward by the size of 1 object.
                //
                ptr = ptr.add(1);
            }
        }
    }

    return [new host.typeSignatureRegistration(myVisualizer, "Simple1DArray")];
}
```

ArrayVisualizer という名前のファイルにスクリプトを保存します。

[**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

Scriptload を使用して、配列ビジュアライザースクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\arrayVisualizer.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\arrayVisualizer.js'
```

これで、dx コマンドを使用すると、スクリプトビジュアライザーに配列の内容の行が表示されます。

```dbgcmd
0:000> dx g_array1D
g_array1D                 : [object Object] [Type: Simple1DArray]
    [<Raw View>]     [Type: Simple1DArray]
    [0x0]            : 0x0
    [0x1]            : 0x1
    [0x2]            : 0x2
    [0x3]            : 0x3
    [0x4]            : 0x4
```

さらに、この JavaScript の視覚化では、Select などの LINQ 機能が提供されています。

```dbgcmd
0:000> dx g_array1D.Select(n => n * 3),d
g_array1D.Select(n => n * 3),d                
    [0]              : 0
    [1]              : 3
    [2]              : 6
    [3]              : 9
    [4]              : 12
```

**視覚エフェクトに影響を与えるもの**

InitializeScript から typeSignatureRegistration オブジェクトを返すことによってネイティブ型のビジュアライザーとして作成されるプロトタイプまたはクラスには、JavaScript 内のすべてのプロパティとメソッドがネイティブ型に追加されます。 また、次のセマンティクスが適用されます。

-   2つのアンダースコア (\_\_) で始まらない名前は、視覚化で使用できるようになります。

-   標準 JavaScript オブジェクトの一部である名前、または JavaScript プロバイダーによって作成されるプロトコルの一部である名前は、視覚化に表示されません。

-   オブジェクトは、\[のシンボル\]のサポートを通じて反復可能なにすることができます。

-   オブジェクトは、getDimensionality、getValueAt、およびオプションで setValueAt の複数の関数で構成されるカスタムプロトコルをサポートすることで、インデックスを作成できます。

**ネイティブオブジェクトブリッジと JavaScript オブジェクトブリッジ**

JavaScript とデバッガーのオブジェクトモデルの間の橋渡しは双方向です。 ネイティブオブジェクトを JavaScript に渡すことができ、JavaScript オブジェクトをデバッガーの式エバリュエーターに渡すことができます。 この例として、スクリプトに次のメソッドを追加することを検討してください。

```javascript
function multiplyBySeven(val)
{
    return val * 7;
}
```

このメソッドは、上記の LINQ クエリ例で使用できるようになりました。 まず、JavaScript の視覚化を読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\arrayVisualizer2.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\arrayVisualizer2.js'

0:000> dx @$myScript = Debugger.State.Scripts.arrayVisualizer2.Contents
```

次に示すように、乗数 Yby7 関数をインラインで使用できます。

```dbgcmd
0:000> dx g_array1D.Select(@$myScript.multiplyBySeven),d
g_array1D.Select(@$myScript.multiplyBySeven),d                
    [0]              : 0
    [1]              : 7
    [2]              : 14
    [3]              : 21
    [4]              : 28
```

## <a name="span-idbreakpointsspanspan-idbreakpointsspanspan-idbreakpointsspanconditional-breakpoints-with-javascript"></a><span id="Breakpoints"></span><span id="breakpoints"></span><span id="BREAKPOINTS"></span>JavaScript を使用した条件付きブレークポイント


ブレークポイントにヒットした後で、JavaScript を使用して補足処理を行うことができます。 たとえば、スクリプトを使用すると、他の実行時の値を調べて、自動的にコードの実行を続行するか停止し、追加の手動デバッグを実行するかどうかを決定できます。

ブレークポイントの操作に関する一般的な情報については、「[ブレークポイントを制御する方法](methods-of-controlling-breakpoints.md)」を参照してください。

**DebugHandler js サンプルブレークポイント処理スクリプト**

この例では、メモ帳の [開く] ダイアログと [保存] ダイアログを評価し*ます。ShowOpenSaveDialog*。 このスクリプトは、pszCaption 変数を評価して、現在のダイアログが [開く] ダイアログであるか、[名前を付けて保存] ダイアログであるかを判断します。 開いているダイアログの場合は、コードの実行が続行されます。 [名前を付けて保存] ダイアログボックスが表示されている場合、コードの実行は停止し、デバッガーは中断します。

```javascript
 // Use JavaScript strict mode 
"use strict";

// Define the invokeScript method to handle breakpoints

 function invokeScript()
 {
    var ctl = host.namespace.Debugger.Utility.Control;

    //Get the address of my string
    var address = host.evaluateExpression("pszCaption");

    // The open and save dialogs use the same function
    // When we hit the open dialog, continue.
    // When we hit the save dialog, break.
    if (host.memory.readWideString(address) == "Open") {
        // host.diagnostics.debugLog("We're opening, let's continue!\n");
        ctl.ExecuteCommand("gc");
    }
    else
    {
        //host.diagnostics.debugLog("We're saving, let's break!\n");
    }
  }
```

[**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load jsprovider.dll
```

このコマンドは、メモ帳にブレークポイントを設定します。ShowOpenSaveDialog は、ブレークポイントにヒットしたときに、上記のスクリプトを実行します。

```dbgcmd
bp notepad!ShowOpenSaveDialog ".scriptrun C:\\WinDbg\\Scripts\\DebugHandler.js"
```

メモ帳で [ファイル &gt; 保存] オプションを選択すると、スクリプトが実行され、g コマンドが送信されず、コードの実行が中断されます。

```dbgcmd
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\DebugHandler.js'
notepad!ShowOpenSaveDialog:
00007ff6`f9761884 48895c2408      mov     qword ptr [rsp+8],rbx ss:000000db`d2a9f2f0=0000021985fe2060
```

## <a name="span-idbitvaluesspanspan-idbitvaluesspanspan-idbitvaluesspanwork-with-64-bit-values-in-javascript-extensions"></a><span id="BitValues"></span><span id="bitvalues"></span><span id="BITVALUES"></span>JavaScript 拡張で64ビット値を使用する


このセクションでは、JavaScript デバッガー拡張機能に渡される64ビット値の動作について説明します。 この問題が発生するのは、JavaScript が53ビットを使用して数値を格納する機能しかないためです。

**64ビットおよび JavaScript 53-ビットストレージ**

JavaScript に渡される序数値は、通常、JavaScript の数値としてマーシャリングされます。 この問題は、JavaScript の数値が64ビットの倍精度浮動小数点値であることです。 53ビットを超える序数は、JavaScript への入力の有効桁数を失います。 これにより、64ビットポインターとその他の64ビット序数値の問題が発生します。これには、最大バイトのフラグが含まれる場合があります。 これに対処するために、JavaScript に入るすべての64ビットネイティブ値 (ネイティブコードまたはデータモデルから) は、JavaScript の数値ではなくライブラリ型として入力します。 このライブラリ型では、数値精度を失うことなく、ネイティブコードにラウンドトリップバックします。

**自動変換**

64ビットの序数値のライブラリ型では、標準の JavaScript 値変換がサポートされています。 オブジェクトが算術演算や、値の変換を必要とするその他のコンストラクトで使用されている場合は、JavaScript の数値に自動的に変換されます。 精度の低下が発生した場合 (値が53ビットを超える序数の精度を利用している場合)、JavaScript プロバイダーは例外をスローします。

JavaScript でビットごとの演算子を使用する場合は、32ビットの序数の有効桁数にさらに制限されていることに注意してください。

このサンプルコードでは、2つの数値を合計し、64ビット値の変換をテストするために使用します。

```javascript
function playWith64BitValues(a64, b64)
{
    // Sum two numbers to demonstrate 64-bit behavior.
    //
    // Imagine a64==100, b64==1000
    // The below would result in sum==1100 as a JavaScript number.  No exception is thrown.  The values auto-convert.
    //
    // Imagine a64==2^56, b64=1
    // The below will **Throw an Exception**.  Conversion to numeric results in loss of precision!
    //
    var sum = a64 + b64;
    host.diagnostics.debugLog("Sum   >> ", sum, "\n");

}

function performOp64BitValues(a64, b64, op)
{
    //
    // Call a data model method passing 64-bit value.  There is no loss of precision here.  This round trips perfectly.
    // For example:
    //  0:000> dx @$myScript.playWith64BitValues(0x4444444444444444ull, 0x3333333333333333ull, (x, y) => x + y)
    //  @$myScript.playWith64BitValues(0x4444444444444444ull, 0x3333333333333333ull, (x, y) => x + y) : 0x7777777777777777
    //
    return op(a64, b64);
}
```

メモ帳などのテキストエディターを使用して、PlayWith64BitValues という名前のテキストファイルを作成し*ます。*

[**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load jsprovider.dll
```

Scriptload コマンドを使用してスクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\PlayWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\PlayWith64BitValues.js'
```

スクリプトを操作しやすくするには、dx コマンドを使用してスクリプトの内容を保持する変数をデバッガーに割り当てます。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.PlayWith64BitValues.Contents
```

Dx 式エバリュエーターを使用して、Addvalues 関数を呼び出します。

最初に、値 2 ^ 53 = 9007199254740992 (16 進 0x20000000000000) を計算します。

まず、(2 ^ 53)-2 を使用して、その合計の値が正しいことを確認します。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740990)
Sum   >> 18014398509481980
```

次に、(2 ^ 53)-1 = 9007199254740991 を計算します。 これにより、変換処理で精度が失われることを示すエラーが返されます。これは、JavaScript コードの sum メソッドで使用できる最大値です。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

64ビット値を渡すデータモデルメソッドを呼び出します。 ここでは精度は失われません。

```dbgcmd
0:001> dx @$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y)
@$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y) : 0xfffffffffffffffe
```

**演算子**

64ビットライブラリの種類は JavaScript オブジェクトであり、JavaScript の数値などの値の型ではありません。 これは、比較操作に何らかの影響を与えます。 通常、オブジェクトの等値 (= =) は、オペランドが同じオブジェクトを参照し、同じ値ではないことを示します。 JavaScript プロバイダーは、64ビット値へのライブ参照を追跡し、収集されていない64ビット値に対して同じ "変更できない" オブジェクトを返すことで、これを軽減します。 これは、比較のために次のようになります。

```javascript
// Comparison with 64 Bit Values

function comparisonWith64BitValues(a64, b64)
{
    //
    // No auto-conversion occurs here.  This is an *EFFECTIVE* value comparison.  This works with ordinals with above 53-bits of precision.
    //
    var areEqual = (a64 == b64);
    host.diagnostics.debugLog("areEqual   >> ", areEqual, "\n");
    var areNotEqual = (a64 != b64);
    host.diagnostics.debugLog("areNotEqual   >> ", areNotEqual, "\n");

    //
    // Auto-conversion occurs here.  This will throw if a64 does not pack into a JavaScript number with no loss of precision.
    //
    var isEqualTo42 = (a64 == 42);
    host.diagnostics.debugLog("isEqualTo42   >> ", isEqualTo42, "\n");
    var isLess = (a64 < b64);
    host.diagnostics.debugLog("isLess   >> ", isLess, "\n");
```

メモ帳などのテキストエディターを使用して、ComparisonWith64BitValues という名前のテキストファイルを作成し*ます。*

[**読み込み (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript プロバイダーを読み込みます。

```dbgcmd
0:000> .load jsprovider.dll
```

Scriptload コマンドを使用してスクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\ComparisonWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\ComparisonWith64BitValues.js'
```

スクリプトを操作しやすくするには、dx コマンドを使用してスクリプトの内容を保持する変数をデバッガーに割り当てます。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.comparisonWith64BitValues.Contents
```

まず、(2 ^ 53)-2 を使用して、予期される値が返されることを確認します。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(9007199254740990, 9007199254740990)
areEqual   >> true
areNotEqual   >> false
isEqualTo42   >> false
isLess   >> false
```

また、必要に応じて比較演算子が動作していることを検証するために、最初の値として数値42を試してみます。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(42, 9007199254740990)
areEqual   >> false
areNotEqual   >> true
isEqualTo42   >> true
isLess   >> true
```

次に、(2 ^ 53)-1 = 9007199254740991 を計算します。 この値は、変換処理によって精度が失われることを示すエラーを返します。これは、JavaScript コードの比較演算子で使用できる最大値です。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

**操作の有効桁数の維持**

デバッガー拡張機能で精度を維持するために、数値演算関数のセットが64ビットライブラリ型の上に射影されます。 拡張機能に必要な有効桁数 (または場合によっては) が64ビットの着信値に対して53ビットを超える必要がある場合は、標準の演算子を使用するのではなく、次のメソッドを使用する必要があります。

|                   |                           |                                                                                                               |
|-------------------|---------------------------|---------------------------------------------------------------------------------------------------------------|
| **メソッド名**   | **折本**             | **説明**                                                                                               |
| asNumber          | .asNumber()               | 64ビット値を JavaScript の数値に変換します。 精度の低下が発生した場合、\*\*例外がスローされ\*\* |
| convertToNumber   | .convertToNumber()        | 64ビット値を JavaScript の数値に変換します。 精度の低下が発生した場合、\*\*例外はスローされません\*\* |
| getLowPart        | .getLowPart()             | 64ビット値の下位32ビットを JavaScript の数値に変換します                                         |
| getHighPart       | .getHighPart()            | 64ビット値の上位32ビットを JavaScript の数値に変換します                                          |
| add               | 。追加 (値)               | 64ビット値に値を加算し、その結果を返します。                                                       |
| 減算 (subtract)          | . 減算 (値)          | 64ビット値から値を減算し、結果を返します。                                                |
| 乗じる          | . 乗算 (値)          | 64ビット値を指定された値で乗算し、結果を返します。                                      |
| 8060            | . 除算 (値)            | 64ビット値を指定された値で除算し、結果を返します。                                         |
| bitwiseAnd        | . bitwiseAnd (値)        | 指定された値を使用して64ビット値のビットごとの and を計算し、結果を返します。                   |
| bitwiseOr         | . bitwiseOr (値)         | 指定された値を使用して64ビット値のビットごとの or を計算し、結果を返します。                    |
| bitwiseXor        | . bitwiseXor (値)        | 指定された値を使用して64ビット値のビットごとの xor を計算し、結果を返します。                   |
| bitwiseShiftLeft  | . bitwiseShiftLeft (値)  | 64ビット値を指定された量だけ左にシフトし、結果を返します                                       |
| bitwiseShiftRight | . bitwiseShiftRight (値) | 64ビット値を指定された量だけ右にシフトし、結果を返します                                      |
| toString          | toString (\[基数\])      | 64ビット値を既定の基数 (または必要に応じて指定された基数) の表示文字列に変換します。         |



## <a name="span-iddebuggingspanspan-iddebuggingspanspan-iddebuggingspanjavascript-debugging"></a><span id="Debugging"></span><span id="debugging"></span><span id="DEBUGGING"></span>JavaScript のデバッグ 

このセクションでは、デバッガーのスクリプトデバッグ機能を使用する方法について説明します。 デバッガーは、 [scriptdebug (Debug javascript)](-scriptdebug--debug-javascript-.md)コマンドを使用した javascript スクリプトのデバッグを統合してサポートしています。

>[!NOTE] 
> WinDbg Preview で JavaScript のデバッグを使用するには、管理者としてデバッガーを実行します。
>


このサンプルコードを使用して、JavaScript のデバッグについて確認します。 このチュートリアルでは、DebuggableSample という名前を付け、C:\MyScripts ディレクトリに保存します。

```javascript
"use strict";

class myObj
{
    toString()
    {
        var x = undefined[42];
        host.diagnostics.debugLog("BOO!\n");
    }
}

class iterObj
{
    *[Symbol.iterator]()
    {
        throw new Error("Oopsies!");
    }
}

function foo()
{
    return new myObj();
}

function iter()
{
    return new iterObj();
}

function throwAndCatch()
{
    var outer = undefined;
    var someObj = {a : 99, b : {c : 32, d: "Hello World"} };
    var curProc = host.currentProcess;
    var curThread = host.currentThread;

    try
    {
        var x = undefined[42];
    } catch(e) 
    {
        outer = e;
    }

    host.diagnostics.debugLog("This is a fun test\n");
    host.diagnostics.debugLog("Of the script debugger\n");
    var foo = {a : 99, b : 72};
    host.diagnostics.debugLog("foo.a = ", foo.a, "\n");

    return outer;
}

function throwUnhandled()
{
    var proc = host.currentProcess;
    var thread = host.currentThread;
    host.diagnostics.debugLog("Hello...  About to throw an exception!\n");
    throw new Error("Oh me oh my!  This is an unhandled exception!\n");
    host.diagnostics.debugLog("Oh...  this will never be hit!\n");
    return proc;
}

function outer()
{
    host.diagnostics.debugLog("inside outer!\n");
    var foo = throwAndCatch();
    host.diagnostics.debugLog("Caught and returned!\n");
    return foo;
}

function outermost()
{
    var x = 99;
    var result = outer();
    var y = 32;
    host.diagnostics.debugLog("Test\n");
    return result;
}

function initializeScript()
{
    //
    // Return an array of registration objects to modify the object model of the debugger
    // See the following for more details:
    //
    //     https://aka.ms/JsDbgExt
    //
}
```

サンプルスクリプトを読み込みます。

```dbgcmd
.scriptload C:\MyScripts\DebuggableSample.js
```

**Scriptdebug**コマンドを使用して、スクリプトのアクティブデバッグを開始します。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

プロンプトが表示されたら *> > > Debug [DebuggableSample <No Position>] >* と入力の要求で、スクリプトデバッガー内にあります。  

JavaScript デバッグ環境でコマンドの一覧を表示するには、 **. help**コマンドを使用します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >.help
Script Debugger Commands (*NOTE* IDs are **PER SCRIPT**):
    ? .................................. Get help
    ? <expr>  .......................... Evaluate expression <expr> and display result
    ?? <expr>  ......................... Evaluate expression <expr> and display result
    |  ................................. List available scripts
    |<scriptid>s  ...................... Switch context to the given script
    bc <bpid>  ......................... Clear breakpoint by specified <bpid>
    bd <bpid>  ......................... Disable breakpoint by specified <bpid>
    be <bpid>  ......................... Enable breakpoint by specified <bpid>
    bl  ................................ List breakpoints
    bp <line>:<column>  ................ Set breakpoint at the specified line and column
    bp <function-name>  ................ Set breakpoint at the (global) function specified by the given name
    bpc  ............................... Set breakpoint at current location
    dv  ................................ Display local variables of current frame
    g  ................................. Continue script
    gu   ............................... Step out
    k  ................................. Get stack trace
    p  ................................. Step over
    q  ................................. Exit script debugger (resume execution)
    sx  ................................ Display available events/exceptions to break on
    sxe <event>  ....................... Enable break on <event>
    sxd <event>  ....................... Disable break on <event>
    t  ................................. Step in
    .attach <scriptId>  ................ Attach debugger to the script specified by <scriptId>
    .detach [<scriptId>]  .............. Detach debugger from the script specified by <scriptId>
    .frame <index>  .................... Switch to frame number <index>
    .f+  ............................... Switch to next stack frame
    .f-  ............................... Switch to previous stack frame
    .help  ............................. Get help
```

**Sx**スクリプトデバッガーコマンドを使用して、トラップできるイベントの一覧を確認します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

**Sxe**スクリプトデバッガーコマンドを使用すると、スクリプトが実行されるコードがすぐにスクリプトデバッガーにトラップされるように、エントリの中断をオンにすることができます。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```


スクリプトデバッガーを終了し、デバッガーにトラップされるスクリプトに関数呼び出しを行います。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >q
```

この時点で、通常のデバッガーに戻ります。  次のコマンドを実行して、スクリプトを呼び出します。

```dbgcmd
dx @$scriptContents.outermost()
```

これで、スクリプトデバッガーに戻り、最も外側にある JavaScript 関数の最初の行で中断されます。  

```dbgcmd
>>> ****** SCRIPT BREAK DebuggableSample [BreakIn] ******   
           Location: line = 73, column = 5                  
           Text: var x = 99                                 

>>> Debug [DebuggableSample 73:5] >                         
```

デバッガーの中断を確認するだけでなく、行 (73) と、中断が発生した列 (5) に加えて、ソースコードの関連するスニペットである*var x = 99*に関する情報を取得します。

いくつかの手順を実行して、スクリプト内の別の場所に移動してみましょう。

```dbgcmd
    p
    t
    p
    t
    p
    p
```

この時点で、34行目の throwAndCatch メソッドに分割する必要があります。  

```dbgcmd
...
>>> ****** SCRIPT BREAK DebuggableSample [Step Complete] ******                       
           Location: line = 34, column = 5                                            
           Text: var curProc = host.currentProcess                                    
```

これを確認するには、スタックトレースを実行します。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

ここでは、変数の値を調べることができます。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >??someObj                
??someObj                                                   
someObj          : {...}                                    
    __proto__        : {...}                                
    a                : 0x63                                 
    b                : {...}                                
>>> Debug [DebuggableSample 34:5] >??someObj.b              
??someObj.b                                                 
someObj.b        : {...}                                    
    __proto__        : {...}                                
    c                : 0x20                                 
    d                : Hello World                          
```

現在のコード行にブレークポイントを設定し、現在設定されているブレークポイントを確認してみましょう。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >bpc                      
bpc                                                         
Breakpoint 1 set at 34:5                                    
>>> Debug [DebuggableSample 34:5] >bl                       
bl                                                          
      Id State    Pos                                       
       1 enabled  34:5                                      
```

ここから、 **sxd**スクリプトデバッガーコマンドを使用して entry (en) イベントを無効にします。 

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

次に、スクリプトを最後まで続行します。

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >g                                                                                   
g                                                                                                                      
This is a fun test                                                                                                     
Of the script debugger                                                                                                 
foo.a = 99                                                                                                             
Caught and returned!                                                                                                   
Test                                                                                                                   
...
```

スクリプトメソッドをもう一度実行し、ブレークポイントにヒットしていることを確認します。

```dbgcmd
0:000> dx @$scriptContents.outermost()                                                
inside outer!                                                                         
>>> ****** SCRIPT BREAK DebuggableSample [Breakpoint 1] ******                        
           Location: line = 34, column = 5                                            
           Text: var curProc = host.currentProcess                                    
```

呼び出し履歴を表示します。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

この時点で、このスクリプトのデバッグを停止します。そのため、このスクリプトからデタッチします。  

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

次に、「q」と入力して終了します。

```dbgcmd                             
q                                                           
This is a fun test                                          
Of the script debugger                                      
foo.a = 99                                                  
Caught and returned!                                        
Test                                                        
```

関数を再度実行しても、デバッガーは中断されなくなります。

```dbgcmd
0:007> dx @$scriptContents.outermost()
inside outer!
This is a fun test
Of the script debugger
foo.a = 99
Caught and returned!
Test
```

## <a name="span-idvscodespanspan-idvscodespanspan-idvscodespanjavascript-in-vscode---adding-intellisense"></a><span id="Vscode"></span><span id="vscode"></span><span id="VSCODE"></span>VSCode での JavaScript-IntelliSense の追加

VSCode でデバッガーデータモデルオブジェクトを操作する場合は、Windows 開発キットで使用できる定義ファイルを使用できます。 IntelliSense 定義ファイルでは、すべてのホスト. * デバッガーオブジェクト Api がサポートされています。 64ビット PC の既定のディレクトリにキットをインストールした場合は、次の場所にあります。

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\JsProvider.d.ts`

VSCode で IntelliSense 定義ファイルを使用するには、次のようにします。

1. 定義ファイル-JSProvider を見つけます。

2. 定義ファイルをスクリプトと同じフォルダーにコピーします。

3. JavaScript スクリプトファイルの先頭に `/// <reference path="JSProvider.d.ts" />` を追加します。

JavaScript ファイルでその参照を使用すると VS Code、スクリプト内の構造に加えて、JSProvider によって提供されるホスト Api に IntelliSense が自動的に与えられます。 たとえば、「host」と入力します。 また、使用可能なすべてのデバッガーモデル Api の IntelliSense が表示されます。


## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanjavascript-resources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>JavaScript リソース


JavaScript のデバッグ拡張機能を開発する際に役立つ可能性のある JavaScript リソースを次に示します。

-   [JavaScript コードの記述](https://docs.microsoft.com/scripting/javascript/writing-javascript-code)

-   [JScript 言語ツアー](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/t895bwkh(v=vs.100))

-   [Mozilla JavaScript リファレンス](https://developer.mozilla.org/docs/Web/JavaScript)

-   [WinJS: JavaScript 用 Windows ライブラリ](https://github.com/winjs/winjs)

-   [ECMAScript 6-新機能: 概要 & 比較](https://es6-features.org/)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[JavaScript デバッガーのサンプルスクリプト](javascript-debugger-example-scripts.md)

[JavaScript 拡張機能のネイティブオブジェクト](native-objects-in-javascript-extensions.md)











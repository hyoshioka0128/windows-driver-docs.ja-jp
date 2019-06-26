---
title: JavaScript デバッガーのスクリプト
description: このトピックでは、JavaScript を使用して、デバッガー オブジェクトについて理解し、拡張、およびデバッガーの機能をカスタマイズするスクリプトを作成する方法について説明します。
ms.assetid: 3442E2C4-4054-4698-B7FB-8FE19D26C171
ms.date: 04/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: aecec2cbf92677e31617a7b17a48178c91a848b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366819"
---
# <a name="javascript-debugger-scripting"></a>JavaScript デバッガーのスクリプト


このトピックでは、JavaScript を使用して、デバッガー オブジェクトについて理解し、拡張、およびデバッガーの機能をカスタマイズするスクリプトを作成する方法について説明します。

## <a name="span-idoverviewofjavascriptdebuggerscriptingspanspan-idoverviewofjavascriptdebuggerscriptingspanspan-idoverviewofjavascriptdebuggerscriptingspanoverview-of-javascript-debugger-scripting"></a><span id="Overview_of_JavaScript_Debugger_Scripting_"></span><span id="overview_of_javascript_debugger_scripting_"></span><span id="OVERVIEW_OF_JAVASCRIPT_DEBUGGER_SCRIPTING_"></span>JavaScript デバッガーがスクリプトの概要


スクリプトのプロバイダーは、デバッガーの内部オブジェクト モデルへのスクリプト言語をブリッジします。 プロバイダー、スクリプト、JavaScript デバッガーを使うと、デバッガーでの JavaScript の使用。

.Scriptload コマンドを使用して、JavaScript が読み込まれると、スクリプトのルート コードが実行される、デバッガー (dx デバッガー) のルート名前空間には、スクリプト内に存在する名前がブリッジおよびアンロードされるまで、スクリプトがメモリに常駐し、そのオブジェクトに対するすべての参照が解放されます。 スクリプトは、新しい機能を提供できる、デバッガーの式エバリュエーターでは、デバッガーでのオブジェクト モデルを変更または同様の NatVis ビジュアライザーはほぼビジュアライザーとして動作できます。

このトピックでは、scripting JavaScript デバッガーで実行できる処理の一部について説明します。

[デバッガーの JavaScript のプロバイダーを読み込む](#provider)

[JavaScript のメタコマンドをスクリプトの使用します。](#commands)

[JavaScript デバッガーがスクリプトの概要します。](#started)

[デバッガー コマンドを自動化します。](#automate)

[JavaScript で条件付きブレークポイントを設定します。](#breakpoints)

[JavaScript でデバッガー ビジュアライザーを作成します。](#visualizer)

[JavaScript の拡張機能内の 64 ビット値を使用します。](#bitvalues)

[JavaScript のデバッグ](#debugging)

[IntelliSense の追加 - VSCode での JavaScript](#vscode)

[JavaScript リソース](#resources)

これら 2 つのトピックでは、デバッガーでの JavaScript の使用に関する追加情報を提供します。

[JavaScript デバッガーの スクリプトの例](javascript-debugger-example-scripts.md)

[JavaScript の拡張機能のネイティブ オブジェクト](native-objects-in-javascript-extensions.md)


## <a name="javascript-scripting-video"></a>JavaScript スクリプト ビデオ

[ツールと 170 をデフラグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-170-Debugger-JavaScript-Scripting)-Andy と請求書は、JavaScript の機能拡張と、デバッガーでの機能をスクリプトを示します。


## <a name="span-idproviderspanspan-idproviderspanspan-idproviderspanthe-debugger-javascript-provider"></a><span id="Provider"></span><span id="provider"></span><span id="PROVIDER"></span>デバッガーの JavaScript プロバイダー

デバッガーに含まれる JavaScript プロバイダー活用 ECMAScript6 のオブジェクトとクラスに関する最新の機能を強化します。 詳細については、次を参照してください。 [ECMAScript 6-新機能。概要 & 比較](https://es6-features.org/)します。

**JsProvider.dll**

JsProvider.dll は、JavaScript デバッガーのスクリプトをサポートするために読み込まれた JavaScript プロバイダーです。

**必要条件**

Windows のサポートされているすべてのバージョンで動作する JavaScript デバッガーのスクリプトは設計されています。

## <a name="span-idloadingthejavascriptscriptingproviderspanspan-idloadingthejavascriptscriptingproviderspanspan-idloadingthejavascriptscriptingproviderspanloading-the-javascript-scripting-provider"></a><span id="Loading_the_JavaScript_Scripting_Provider"></span><span id="loading_the_javascript_scripting_provider"></span><span id="LOADING_THE_JAVASCRIPT_SCRIPTING_PROVIDER"></span>JavaScript のプロバイダーをスクリプトの読み込み


スクリプトのプロバイダーを .script コマンドのいずれかを使用するのを使用して読み込む必要があります、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンド。 JavaScript のプロバイダーを読み込むには、次のコマンドを使用します。

```dbgcmd
0:000> .load jsprovider.dll
```

.Scriptproviders コマンドを使用して、JavaScript のプロバイダーが読み込まれていることを確認します。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

## <a name="span-idcommandsspanspan-idcommandsspanspan-idcommandsspanjavascript-scripting-meta-commands"></a><span id="Commands"></span><span id="commands"></span><span id="COMMANDS"></span>JavaScript スクリプト コマンド


次のコマンドは、JavaScript デバッガーのスクリプトで使用できます。

-   [ **.scriptproviders (スクリプト プロバイダーの一覧)** ](-scriptproviders--list-script-providers-.md)
-   [ **.scriptload (スクリプトの読み込み)** ](-scriptload--load-script-.md)
-   [ **.scriptunload (アンロード スクリプト)** ](-scriptunload--unload-script-.md)
-   [ **.scriptrun (スクリプトの実行)** ](-scriptrun--run-script-.md)
-   [ **.scriptlist (読み込まれたスクリプトを一覧表示)** ](-scriptlist--list-loaded-scripts-.md)

**必要条件**

スクリプトのプロバイダーを .script コマンドのいずれかを使用するのを使用して読み込む必要があります、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンド。 JavaScript のプロバイダーを読み込むには、次のコマンドを使用します。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idscriptproviderslistscriptprovidersspanspan-idscriptproviderslistscriptprovidersspanscriptproviders-list-script-providers"></a><span id=".scriptproviders__list_script_providers_"></span><span id=".SCRIPTPROVIDERS__LIST_SCRIPT_PROVIDERS_"></span>.scriptproviders (スクリプト プロバイダーの一覧)


.Scriptproviders コマンドには、デバッガーとする登録されている拡張機能によって現在認識されているすべてのスクリプト言語が一覧表示します。

次の例では、JavaScript と NatVis プロバイダーが読み込まれます。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

終わるすべてのファイル"です。NatVis"は、NatVis スクリプトと考えるし、".js"で終わるすべてのファイルが JavaScript スクリプトとして認識します。 .Scriptload コマンドを使用してスクリプトのいずれかの型を読み込むことができます。

詳細については、次を参照してください[ **.scriptproviders (スクリプト プロバイダーの一覧)。** ](-scriptproviders--list-script-providers-.md)

## <a name="span-idscriptloadloadscriptspanspan-idscriptloadloadscriptspanscriptload-load-script"></a><span id=".scriptload__load_script_"></span><span id=".SCRIPTLOAD__LOAD_SCRIPT_"></span>.scriptload (スクリプトの読み込み)


.Scriptload コマンドはスクリプトを読み込むし、スクリプトのルート コードを実行し、 *initializeScript*関数。 初期読み込みと、スクリプトの実行でエラーがある場合、エラーが表示されますコンソールにします。 次のコマンドは、TestScript.js の読み込みが成功したを示しています。

```dbgcmd
0:000> .scriptload C:\WinDbg\Scripts\TestScript.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\TestScript.js'
```

スクリプトによって行われたすべてのオブジェクト モデル操作は、スクリプトが読み込まれた後または別のコンテンツを再度実行するまで、場所に維持されます。

詳細については、次を参照してください[ **.scriptload (スクリプトの読み込み)。** ](-scriptload--load-script-.md)

## <a name="span-idscriptrunspanscriptrun"></a><span id=".SCRIPTRUN"></span>.scriptrun


.Scriptrun コマンドはスクリプトを読み込むのスクリプトのルート コードを実行、 *initializeScript*と*invokeScript*関数。 初期読み込みと、スクリプトの実行でエラーがある場合、エラーが表示されますコンソールにします。

```dbgcmd
0:000> .scriptrun C:\WinDbg\Scripts\helloWorld.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\helloWorld.js'
Hello World!  We are in JavaScript!
```

スクリプトによって行われたすべてのデバッガー オブジェクト モデルの操作は、スクリプトが読み込まれた後または別のコンテンツを再度実行するまで、場所に維持されます。

詳細については、次を参照してください。 [ **.scriptrun (スクリプトの実行)** ](-scriptrun--run-script-.md)します。

## <a name="span-idscriptunloadunloadscriptspanspan-idscriptunloadunloadscriptspanscriptunload-unload-script"></a><span id=".scriptunload__unload_script_"></span><span id=".SCRIPTUNLOAD__UNLOAD_SCRIPT_"></span>.scriptunload (アンロード スクリプト)


.Scriptunload コマンドが読み込まれているスクリプトと呼び出しをアンロード、 *uninitializeScript*関数。 次のコマンド構文を使用して、スクリプトをアンロードするには

```dbgcmd
0:000:x86> .scriptunload C:\WinDbg\Scripts\TestScript.js
JavaScript script unloaded from 'C:\WinDbg\Scripts\TestScript.js'
```

詳細については、次を参照してください。 [ **.scriptunload (アンロード スクリプト)** ](-scriptunload--unload-script-.md)します。

## <a name="span-idscriptlistlistloadedscriptsspanspan-idscriptlistlistloadedscriptsspanscriptlist-list-loaded-scripts"></a><span id=".scriptlist__list_loaded_scripts_"></span><span id=".SCRIPTLIST__LIST_LOADED_SCRIPTS_"></span>.scriptlist (読み込まれたスクリプトを一覧表示)


.Scriptlist コマンドには、.scriptload または .scriptrun コマンドを使用して読み込まれているすべてのスクリプトが表示されます。 .Scriptload を使用して、TestScript が読み込み成功した場合、.scriptlist コマンドは、読み込まれたスクリプトの名前を表示します。

```dbgcmd
0:000> .scriptlist
Command Loaded Scripts:
    JavaScript script from 'C:\WinDbg\Scripts\TestScript.js'
```

詳細については、次を参照してください。 [ **.scriptlist (読み込まれたスクリプトの一覧)** ](-scriptlist--list-loaded-scripts-.md)します。

## <a name="span-idstartedspanspan-idstartedspanspan-idstartedspanget-started-with-javascript-debugger-scripting"></a><span id="Started"></span><span id="started"></span><span id="STARTED"></span>JavaScript デバッガーがスクリプトの概要します。


### <a name="span-idhelloworldexamplescriptspanspan-idhelloworldexamplescriptspanspan-idhelloworldexamplescriptspanhelloworld-example-script"></a><span id="HelloWorld_Example_Script"></span><span id="helloworld_example_script"></span><span id="HELLOWORLD_EXAMPLE_SCRIPT"></span>HelloWorld サンプル スクリプト

このセクションでは、作成し、Hello World を出力する単純な JavaScript デバッガー スクリプトを実行する方法について説明します。

```dbgcmd
// WinDbg JavaScript sample
// Prints Hello World
function initializeScript()
{
    host.diagnostics.debugLog("***> Hello World! \n");
}
```

という名前のテキスト ファイルを作成するには、メモ帳などのテキスト エディターを使用して*HelloWorld.js*上記の JavaScript コードを格納しています。

使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

.Scriptload コマンドを使用して、読み込み、スクリプトを実行します。 関数名を使用しているため*initializeScript*スクリプトが読み込まれるときに、関数のコードを実行します。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\HelloWorld.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\HelloWorld.js'
***> Hello World! 
```

スクリプトが読み込まれた後、追加の機能がデバッガーで使用します。 使用して、 [ **dx (NatVis 式の表示)** ](dx--display-visualizer-variables-.md)コマンドを表示する*Debugger.State.Scripts*スクリプトが常駐しているようになりましたことを確認します。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    HelloWorld 
```

次の例では追加し、名前付き関数を呼び出します。

### <a name="span-idaddingtwovaluesexamplescriptspanspan-idaddingtwovaluesexamplescriptspanspan-idaddingtwovaluesexamplescriptspanadding-two-values-example-script"></a><span id="Adding_Two_Values_Example_Script"></span><span id="adding_two_values_example_script"></span><span id="ADDING_TWO_VALUES_EXAMPLE_SCRIPT"></span>2 つの値の例のスクリプトを追加します。

このセクションでは、作成し、単純な JavaScript を追加するデバッガー スクリプトの入力を受け取り、2 つの数値を加算を実行する方法について説明します。

この単純なスクリプトでは、1 つの関数、addTwoValues を提供します。

```dbgcmd
// WinDbg JavaScript sample
// Adds two functions
function addTwoValues(a, b)
 {
     return a + b;
 }
```

という名前のテキスト ファイルを作成するには、メモ帳などのテキスト エディターを使用して*FirstSampleFunction.js*

使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

.Scriptload コマンドを使用して、スクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

スクリプトが読み込まれた後、追加の機能がデバッガーで使用します。 使用して、 [ **dx (NatVis 式の表示)** ](dx--display-visualizer-variables-.md)コマンドを表示する*Debugger.State.Scripts*スクリプトが常駐しているようになりましたことを確認します。

```dbgcmd
0:000> dx Debugger.State.Scripts
Debugger.State.Scripts                
    FirstSampleFunction    
```

ボタンをクリックする、 *FirstSampleFunction*、して、どのような機能を提供します。

```dbgcmd
0:000> dx -r1 -v Debugger.State.Scripts.FirstSampleFunction.Contents
Debugger.State.Scripts.FirstSampleFunction.Contents                 : [object Object]
    host             : [object Object]
    addTwoValues    
 ... 
```

スクリプトを少し簡単に操作できるようにするには、dx コマンドを使用してスクリプトの内容を保持するために、デバッガーの変数を割り当てます。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.FirstSampleFunction.Contents
```

Dx 式エバリュエーターを使用して、addTwoValues 関数を呼び出します。

```dbgcmd
0:000> dx @$myScript.addTwoValues(10, 41),d
@$myScript.addTwoValues(10, 41),d : 51
```

使用することも、 *@$ scriptContents*スクリプトを使用するエイリアスに組み込まれています。 *@$ ScriptContents*すべてのエイリアスにマージします。読み込まれたスクリプトのすべてのコンテンツ。

```dbgcmd
0:001> dx @$scriptContents.addTwoValues(10, 40),d
@$scriptContents.addTwoValues(10, 40),d : 50
```

完了したら、スクリプトの操作 .scriptunload コマンドを使用して、スクリプトをアンロードします。

```dbgcmd
0:000> .scriptunload c:\WinDbg\Scripts\FirstSampleFunction.js
JavaScript script successfully unloaded from 'c:\WinDbg\Scripts\FirstSampleFunction.js'
```

### <a name="span-idautomatespanspan-idautomatespanspan-idautomatespandebugger-command-automation"></a><span id="Automate"></span><span id="automate"></span><span id="AUTOMATE"></span>デバッガー コマンドの自動化

このセクションを作成しの送信を自動化する単純な JavaScript デバッガー スクリプトを実行する方法を説明します、 [ **u (Unassemble)** ](u--unassemble-.md)コマンド。 このサンプルでは、収集し、ループ内でコマンドの出力を表示する方法も示します。

このスクリプトでは、1 つの関数、RunCommands() を提供します。

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

という名前のテキスト ファイルを作成するには、メモ帳などのテキスト エディターを使用して*RunCommands.js*

使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

.Scriptload コマンドを使用して、RunCommands スクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\RunCommands.js 
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\RunCommands.js'
```

スクリプトが読み込まれた後、追加の機能がデバッガーで使用します。 使用して、 [ **dx (NatVis 式の表示)** ](dx--display-visualizer-variables-.md)コマンドを表示する*Debugger.State.Scripts.RunCommands*スクリプトが常駐しているようになりましたことを確認します。

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

Dx コマンドを使用して、RunCommands スクリプトで RunCommands 関数を呼び出します。

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

## <a name="span-idspecialjavascriptdebuggerfunctionsspanspan-idspecialjavascriptdebuggerfunctionsspanspan-idspecialjavascriptdebuggerfunctionsspanspecial-javascript-debugger-functions"></a><span id="Special_JavaScript_Debugger_Functions"></span><span id="special_javascript_debugger_functions"></span><span id="SPECIAL_JAVASCRIPT_DEBUGGER_FUNCTIONS"></span>特別な JavaScript デバッガー関数


スクリプト プロバイダー自体によって呼び出される JavaScript スクリプトには、いくつかの特殊な関数があります。

### <a name="span-idinitializescriptspanspan-idinitializescriptspanspan-idinitializescriptspaninitializescript"></a><span id="initializeScript"></span><span id="initializescript"></span><span id="INITIALIZESCRIPT"></span>initializeScript

とき JavaScript スクリプトが読み込まれたとは、実行すると、一連の変数、関数前に、の手順をスクリプトで他のオブジェクトは、デバッガーのオブジェクト モデルに影響します。

-   スクリプトがメモリに読み込まれ、解析します。
-   スクリプト内のルート コードが実行されます。
-   スクリプトに initializeScript という名前のメソッドがある場合は、このメソッドが呼び出されます。
-   InitializeScript からの戻り値はデバッガーのオブジェクト モデルを自動的に変更する方法を決定するために使用します。
-   デバッガーの名前空間には、スクリプト内の名前がブリッジされます。

前述のように、initializeScript はスクリプトのルート コードが実行された直後後に呼び出されます。 そのジョブでは、デバッガーのオブジェクト モデルを変更する方法を示す、プロバイダーに登録オブジェクトの JavaScript 配列を返します。

```javascript
function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> initializeScript was called\n");
}
```

### <a name="span-idinvokescriptspanspan-idinvokescriptspanspan-idinvokescriptspaninvokescript"></a><span id="invokeScript"></span><span id="invokescript"></span><span id="INVOKESCRIPT"></span>invokeScript

InvokeScript メソッドは、プライマリ スクリプト メソッドで .scriptload と .scriptrun が実行時に呼び出されます。

```javascript
function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> invokeScript was called\n");
}
```

### <a name="span-iduninitializescriptspanspan-iduninitializescriptspanspan-iduninitializescriptspanuninitializescript"></a><span id="uninitializeScript"></span><span id="uninitializescript"></span><span id="UNINITIALIZESCRIPT"></span>uninitializeScript

UninitializeScript メソッドは、initializeScript の行動の反対です。 スクリプトがリンクと、アンロードする準備が呼び出されます。 そのジョブは、スクリプトが実行中に強制的に使用した、オブジェクト モデルへの変更を元に戻す、またはスクリプトがキャッシュされている任意のオブジェクトを破棄するには。

スクリプト オブジェクト モデルへの命令型の操作も、結果をキャッシュする場合、は、uninitializeScript メソッドがあることが必要はありません。 実行 initializeScript の戻り値で示されているオブジェクト モデルへの変更は、プロバイダーによって自動的に元に戻します。 このような変更では、明示的な uninitializeScript メソッドは必要ありません。

```javascript
function uninitializeScript()
{
    // Add code here that you want to run every time the script is unloaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***> uninitialize was called\n");
}
```

## <a name="span-idsummaryoffunctionscalledbyscriptcommandsspanspan-idsummaryoffunctionscalledbyscriptcommandsspanspan-idsummaryoffunctionscalledbyscriptcommandsspansummary-of-functions-called-by-script-commands"></a><span id="Summary_of_Functions_Called_by_Script_Commands"></span><span id="summary_of_functions_called_by_script_commands"></span><span id="SUMMARY_OF_FUNCTIONS_CALLED_BY_SCRIPT_COMMANDS"></span>スクリプト コマンドによって呼び出された関数の概要


この表では、スクリプト コマンドによってどの関数が呼び出される

||[.scriptload](-scriptload--load-script-.md)|[.scriptrun (スクリプトの実行)](-scriptrun--run-script-.md)|[.scriptunload (アンロード スクリプト)](-scriptunload--unload-script-.md)|
|--- |--- |--- |--- |
|ルート|○|○| | |
|initializeScript|○|○| | |
|invokeScript       | |○| |
|uninitializeScript | ||はい|


このサンプル コードを使用して、各関数が呼び出されると、スクリプトは読み込まれ、実行、アンロードを参照してください。

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

## <a name="span-idvisualizerspanspan-idvisualizerspanspan-idvisualizerspancreating-a-debugger-visualizer-in-javascript"></a><span id="Visualizer"></span><span id="visualizer"></span><span id="VISUALIZER"></span>JavaScript でデバッガー ビジュアライザーを作成します。


カスタム ビジュアル ファイルを使用すると、グループ化およびデータ間の関係とコンテンツを正確に反映させた視覚エフェクトの構造内のデータを整理できます。 JavaScript デバッガー拡張機能を使用して、非常に NatVis と同様の方法で操作を実行するデバッガー ビジュアライザーを記述することができます。 これは、特定のデータ ビジュアライザーとして機能する入力、JavaScript プロトタイプ オブジェクト (または、ES6 クラス) の作成を使用して実現されます。 NatVis とデバッガーの詳細については、次を参照してください。 [ **dx (表示 NatVis 式)** ](dx--display-visualizer-variables-.md)します。

**クラスの例 - Simple1DArray**

1 次元配列を表す C++ クラスの例を検討してください。 このクラスには 2 つのメンバーでは、m\_サイズは、配列、および m の全体的なサイズ\_pValues メモリ内の整数の数値へのポインターであると等しく、m\_サイズ フィールド。

```cpp
class Simple1DArray
{
private:

    ULONG64 m_size;
    int *m_pValues;
};
```

Dx コマンドを使用して、既定のデータ構造の表示を確認することできます。

```dbgcmd
0:000> dx g_array1D
g_array1D                 [Type: Simple1DArray]
    [+0x000] m_size           : 0x5 [Type: unsigned __int64]
    [+0x008] m_pValues        : 0x8be32449e0 : 0 [Type: int *]
```

**JavaScript のビジュアライザー**

この型を視覚化するために作成者のプロトタイプ (または ES6) クラスを持つすべてのフィールドに必要があります。 および、デバッガーを表示するプロパティ。 また、initializeScript メソッドを指定した型のビジュアライザーとして、プロトタイプをリンクする JavaScript プロバイダーに指示するオブジェクトを返す必要があります。

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

ArrayVisualizer.js という名前のファイル、スクリプトを保存します。

使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

.Scriptload を使用して、配列のビジュアライザーのスクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\arrayVisualizer.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\arrayVisualizer.js'
```

ここで、dx コマンドを使用する場合は、配列の内容の行をスクリプト ビジュアライザーに表示されます。

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

さらに、この JavaScript の視覚エフェクトは、Select などの LINQ 機能を提供します。

```dbgcmd
0:000> dx g_array1D.Select(n => n * 3),d
g_array1D.Select(n => n * 3),d                
    [0]              : 0
    [1]              : 3
    [2]              : 6
    [3]              : 9
    [4]              : 12
```

**視覚エフェクトへの影響について**

プロトタイプまたは initializeScript の host.typeSignatureRegistration オブジェクトの戻り値によって、ネイティブ型のビジュアライザーで構成されるクラスを持つすべてのプロパティと、JavaScript 内のメソッドは、ネイティブな型に追加します。 さらに、次のセマンティクスが適用されます。

-   2 つのアンダー スコアで始まっていないを任意の名前 (\_\_) は、視覚エフェクトで利用できます。

-   標準の JavaScript オブジェクトの一部であるか、JavaScript のプロバイダーを作成するプロトコルの一部である名前も、視覚化に表示されません。

-   オブジェクトのサポートを利用して反復可能なできる\[Symbol.iterator\]します。

-   オブジェクトをいくつかの関数で構成されるカスタム プロトコルのサポートを利用してインデックス付けできる: getDimensionality、getValueAt、および必要に応じて setValueAt します。

**ネイティブおよび JavaScript オブジェクトのブリッジ**

JavaScript とデバッガーのオブジェクト モデル間のブリッジでは、双方向です。 JavaScript にネイティブなオブジェクトを渡すことができ、デバッガーの式エバリュエーターに JavaScript オブジェクトを渡すことができます。 これの例は、としては、このスクリプトでは、次のメソッドの追加を検討してください。

```javascript
function multiplyBySeven(val)
{
    return val * 7;
}
```

このメソッドは、上記の例の LINQ クエリで今すぐ利用できます。 まず、JavaScript の視覚エフェクトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\arrayVisualizer2.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\arrayVisualizer2.js'

0:000> dx @$myScript = Debugger.State.Scripts.arrayVisualizer2.Contents
```

次の関数のインラインでは、次に示す multiplyBySeven を使用できます。

```dbgcmd
0:000> dx g_array1D.Select(@$myScript.multiplyBySeven),d
g_array1D.Select(@$myScript.multiplyBySeven),d                
    [0]              : 0
    [1]              : 7
    [2]              : 14
    [3]              : 21
    [4]              : 28
```

## <a name="span-idbreakpointsspanspan-idbreakpointsspanspan-idbreakpointsspanconditional-breakpoints-with-javascript"></a><span id="Breakpoints"></span><span id="breakpoints"></span><span id="BREAKPOINTS"></span>JavaScript での条件付きブレークポイント


ブレークポイントにヒットした後に、補足処理を行うには、JavaScript を使用できます。 たとえば、スクリプトは、その他の実行時の値を確認し、自動的にコードの実行を継続または停止して追加の手動デバッグを実行するかを使用できます。

ブレークポイントの操作方法の概要については、次を参照してください。[ブレークポイントの制御メソッド](methods-of-controlling-breakpoints.md)します。

**ブレークポイントの処理のスクリプトを DebugHandler.js 例**

この例は、メモ帳のオープンを評価し、保存ダイアログ:*メモ帳!ShowOpenSaveDialog*します。 このスクリプトでは、現在のダイアログ ボックスが 開く ダイアログ ボックスの場合、または"名前を付けて保存 ダイアログ ボックスである場合を判断する pszCaption 変数を評価します。 かどうか、[開く] ダイアログは、コードの実行が継続されます。 付けて保存 ダイアログの場合、コードの実行は停止しデバッガーが中断します。

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

使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

このコマンドは、メモ帳にブレークポイントを設定します。ShowOpenSaveDialog、そのブレークポイントはヒットたびに、上記のスクリプトを実行するとします。

```dbgcmd
bp notepad!ShowOpenSaveDialog ".scriptrun C:\\WinDbg\\Scripts\\DebugHandler.js"
```

その後、ファイル&gt;メモ帳で保存オプションが選択されている、スクリプトを実行、g コマンドは送信されず、およびコードの実行の中断が発生します。

```dbgcmd
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\DebugHandler.js'
notepad!ShowOpenSaveDialog:
00007ff6`f9761884 48895c2408      mov     qword ptr [rsp+8],rbx ss:000000db`d2a9f2f0=0000021985fe2060
```

## <a name="span-idbitvaluesspanspan-idbitvaluesspanspan-idbitvaluesspanwork-with-64-bit-values-in-javascript-extensions"></a><span id="BitValues"></span><span id="bitvalues"></span><span id="BITVALUES"></span>JavaScript の拡張機能内の 64 ビット値を使用します。


このセクションに渡された値を 64 ビットの方法を説明します JavaScript デバッガー拡張機能が動作します。 JavaScript は 53 ビットを使用して数値を格納する機能のみが、この問題が発生します。

**64 ビットと 53 ビットのストレージの JavaScript**

JavaScript に渡された序数値は、JavaScript の数値として通常マーシャ リングされます。 この問題は、JavaScript の数値が 64 ビットの倍精度浮動小数点値です。 53 ビット経由で任意の序数は JavaScript への入力に精度が失われます。 これは、64 ビット ポインターと最上位バイトにフラグがあります。 その他の 64 ビット序数値の問題を表示します。 これに対処するためには、64 ビット ネイティブ値 (ネイティブ コードまたはデータ モデルからかどうか) が JavaScript の入力は、JavaScript の数値としてではなく - ライブラリの種類として入力します。 このライブラリの種類は、数値有効桁数を失うことがなくネイティブ コードに戻るラウンド トリップをされます。

**自動変換**

ライブラリは、64 ビットの序数値の種類には、標準の JavaScript valueOf 変換がサポートしています。 算術演算または値の変換を必要とする他の構造体で、オブジェクトを使用する場合は、JavaScript の数値に自動的に変換します。 有効桁数の損失が発生した場合 (値を利用 53 ビットの序数の有効桁数を超える)、JavaScript プロバイダー例外がスローされます。

注意してください、JavaScript でビットごとの演算子を使用する場合さらに、序数に基づく精度の 32 ビットに制限されます。

このサンプル コードでは、2 つの数値を合計して、64 ビット値の変換をテストするために使用されます。

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

という名前のテキスト ファイルを作成するには、メモ帳などのテキスト エディターを使用して*PlayWith64BitValues.js*

使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

.Scriptload コマンドを使用して、スクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\PlayWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\PlayWith64BitValues.js'
```

スクリプトを少し簡単に操作できるようにするには、dx コマンドを使用してスクリプトの内容を保持するために、デバッガーの変数を割り当てます。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.PlayWith64BitValues.Contents
```

Dx 式エバリュエーターを使用して、addTwoValues 関数を呼び出します。

2 の値を計算します最初 ^53 = 9007199254740992 (16 進 0x20000000000000)。

最初にテストするには使用 (2 ^53) - 2 と合計の正しい値が返されるを参照してください。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740990)
Sum   >> 18014398509481980
```

計算は、(2 ^53)-1 9007199254740991 を = です。 これは、JavaScript コードで sum メソッドを使用できる最大値に変換プロセスが有効桁数を失うことを示すエラーが返されます。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

64 ビット値を渡すデータ モデルのメソッドを呼び出します。 ここでの有効桁数の損失はありません。

```dbgcmd
0:001> dx @$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y)
@$myScript.performOp64BitValues( 0x7FFFFFFFFFFFFFFF,  0x7FFFFFFFFFFFFFFF, (x, y) => x + y) : 0xfffffffffffffffe
```

**比較**

64 ビット ライブラリ型は、JavaScript オブジェクトと、JavaScript の数値などの値型ではなくです。 これにより、比較操作の影響があります。 通常、オブジェクトの等価 (= =) では、オペランドが同じオブジェクトと同じ値ではなくを参照していることを示します。 JavaScript のプロバイダーは、64 ビット値へのライブ参照を追跡し、64 ビット値の収集以外の場合は、同じ「変更できない」オブジェクトを返すことでこれを軽減します。 つまり、比較については、次が発生します。

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

という名前のテキスト ファイルを作成するには、メモ帳などのテキスト エディターを使用して*ComparisonWith64BitValues.js*

使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

.Scriptload コマンドを使用して、スクリプトを読み込みます。

```dbgcmd
0:000> .scriptload c:\WinDbg\Scripts\ComparisonWith64BitValues.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\ComparisonWith64BitValues.js'
```

スクリプトを少し簡単に操作できるようにするには、dx コマンドを使用してスクリプトの内容を保持するために、デバッガーの変数を割り当てます。

```dbgcmd
0:000> dx @$myScript = Debugger.State.Scripts.comparisonWith64BitValues.Contents
```

最初にテストするには使用 (2 ^53) - 2 と予期される値を返すことを参照してください。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(9007199254740990, 9007199254740990)
areEqual   >> true
areNotEqual   >> false
isEqualTo42   >> false
isLess   >> false
```

数字「42 が比較演算子を検証する最初値を使用している必要があります私たちも試行されます。

```dbgcmd
0:001> dx @$myScript.comparisonWith64BitValues(42, 9007199254740990)
areEqual   >> false
areNotEqual   >> true
isEqualTo42   >> true
isLess   >> true
```

計算は、(2 ^53)-1 9007199254740991 を = です。 この値は、これは、JavaScript コードで比較演算子と共に使用できる最大値に変換プロセスが有効桁数を失うことを示すエラーを返します。

```dbgcmd
0:000> dx @$myScript.playWith64BitValues(9007199254740990, 9007199254740991)
Error: 64 bit value loses precision on conversion to number
```

**操作の有効桁数の維持**

精度を維持するためにデバッガー拡張機能を許可するためには、一連の数値演算関数は、64 ビット ライブラリの種類の上に射影されます。 拡張機能必要があります (または可能性がある可能性があります) 必要がある場合 53 ビット上の有効桁数の受信の 64 ビット値、標準の演算子ではなく、次のメソッドを利用する必要があります。

|                   |                           |                                                                                                               |
|-------------------|---------------------------|---------------------------------------------------------------------------------------------------------------|
| **メソッド名**   | **署名**             | **[説明]**                                                                                               |
| asNumber          | .asNumber()               | 64 ビット値を JavaScript の数値に変換します。 有効桁数の損失が発生した場合\*\*例外がスローされます\*\* |
| convertToNumber   | .convertToNumber()        | 64 ビット値を JavaScript の数値に変換します。 有効桁数の損失が発生した場合\*\*いいえ例外がスローされます\*\* |
| getLowPart        | .getLowPart()             | 64 ビット値の下位 32 ビットを JavaScript の数値に変換します。                                         |
| getHighPart       | .getHighPart()            | 64 ビット値の上位 32 ビットを JavaScript の数値に変換します。                                          |
| 追加               | .add(value)               | 64 ビット値に値を追加し、結果を返します                                                       |
| 減算 (subtract)          | .subtract(value)          | 64 ビットの値から値を減算し、結果を返します                                                |
| 乗算          | .multiply(value)          | 指定された値では、64 ビット値を乗算し、結果を返します                                      |
| 除算            | .divide(value)            | 64 ビット値を指定された値で除算し、結果を返します                                         |
| BitwiseAnd        | .bitwiseAnd(value)        | 64 ビット値が指定された値の積を計算し、結果を返します                   |
| BitwiseOr         | .bitwiseOr(value)         | ビットまたは 64 ビット値が指定された値の計算し、結果を返します                    |
| bitwiseXor        | .bitwiseXor(value)        | 指定された値と 64 ビット値のビットごとの xor を計算し、結果を返します                   |
| bitwiseShiftLeft  | .bitwiseShiftLeft(value)  | 64 ビット値が指定された数だけ左にシフトし、結果を返します                                       |
| bitwiseShiftRight | .bitwiseShiftRight(value) | 64 ビット値を指定した量だけ右にシフトし、結果を返します                                      |
| ToString          | .toString(\[radix\])      | 64 ビット値を既定の基数 (またはオプションで指定した基数) での表示文字列に変換します。         |



## <a name="span-iddebuggingspanspan-iddebuggingspanspan-iddebuggingspanjavascript-debugging"></a><span id="Debugging"></span><span id="debugging"></span><span id="DEBUGGING"></span>JavaScript のデバッグ 

このセクションでは、デバッグ、デバッガーの機能のスクリプトを使用する方法について説明します。 デバッガーを使用して JavaScript スクリプトをデバッグするためのサポートが統合された、 [.scriptdebug (JavaScript のデバッグ)](-scriptdebug--debug-javascript-.md)コマンド。

>[!NOTE] 
> WinDbg のプレビューでは、JavaScript のデバッグを使用するには、管理者として、デバッガーを実行します。
>


このサンプル コードを使用して、JavaScript のデバッグを検証します。 このチュートリアルでは DebuggableSample.js という名前を付けますがお C:\MyScripts ディレクトリに保存します。

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

サンプル スクリプトを読み込みます。

```dbgcmd
.scriptload C:\MyScripts\DebuggableSample.js
```

スクリプトを使用して、積極的にデバッグを開始、 **.scriptdebug**コマンド。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

プロンプトが表示されたら *>>> デバッグ [DebuggableSample <No Position>] >* スクリプト デバッガー内では入力を要求します。  

使用して、 **.help** JavaScript のデバッグ環境でコマンドの一覧を表示するコマンド。

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

使用して、 **sx**こと、トラップできるイベントの一覧を表示するデバッガー コマンドのスクリプトを作成します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

使用して、 **sxe**内に任意のコードが実行されるとすぐにスクリプト デバッガーに、スクリプトをトラップするためのエントリをブレークをオンにするデバッガー コマンドのスクリプトを作成します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```


スクリプト デバッガーを終了して、関数をデバッガーにトラップがスクリプトに呼び出しを行います。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >q
```

この時点では、通常のデバッガーにしています。  スクリプトを呼び出す次のコマンドを実行します。

```dbgcmd
dx @$scriptContents.outermost()
```

これで、スクリプト デバッガーに戻ってが最も外側の JavaScript 関数の 1 行目で壊れているとします。  

```dbgcmd
>>> ****** SCRIPT BREAK DebuggableSample [BreakIn] ******   
           Location: line = 73, column = 5                  
           Text: var x = 99                                 

>>> Debug [DebuggableSample 73:5] >                         
```

デバッガーにブレークを表示することに加えて、行 (73) で、中断が場所とソース コードの関連するスニペットを要した列 (5) の情報を取得する: *var x 99*します。

数回の手順をスクリプトの別の場所を取得しましょう。

```dbgcmd
    p
    t
    p
    t
    p
    p
```

この時点では、34 行目で throwAndCatch メソッドに分割する必要があります。  

```dbgcmd
...
>>> ****** SCRIPT BREAK DebuggableSample [Step Complete] ******                       
           Location: line = 34, column = 5                                            
           Text: var curProc = host.currentProcess                                    
```

スタック トレースを実行することによって、これを確認することができます。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

ここでは、変数の値を調査できます。

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

現在のコード行にブレークポイントを設定して、どのようなブレークポイントを設定して今すぐ参照してください。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >bpc                      
bpc                                                         
Breakpoint 1 set at 34:5                                    
>>> Debug [DebuggableSample 34:5] >bl                       
bl                                                          
      Id State    Pos                                       
       1 enabled  34:5                                      
```

ここを無効にします (en) のエントリのイベントを使用、 **sxd**デバッガー コマンドのスクリプトを作成します。 

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

だけ移動し、スクリプトの最後まで続行します。

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

スクリプト メソッドをもう一度実行し、ヒットするブレークポイントを確認します。

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

この時点では、そこからデタッチしますので、このスクリプトのデバッグを停止します。  

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

Q を押して終了を入力します。

```dbgcmd                             
q                                                           
This is a fun test                                          
Of the script debugger                                      
foo.a = 99                                                  
Caught and returned!                                        
Test                                                        
```

関数をもう一度実行は、デバッガーに割り込むが不要になった。

```dbgcmd
0:007> dx @$scriptContents.outermost()
inside outer!
This is a fun test
Of the script debugger
foo.a = 99
Caught and returned!
Test
```

## <a name="span-idvscodespanspan-idvscodespanspan-idvscodespanjavascript-in-vscode---adding-intellisense"></a><span id="Vscode"></span><span id="vscode"></span><span id="VSCODE"></span>IntelliSense の追加 - VSCode での JavaScript

VSCode でデバッガーのデータ モデル オブジェクトを操作したい場合は、Windows の開発キットで提供される定義ファイルを使用できます。 IntelliSense の定義ファイルでは、すべて host.* デバッガー オブジェクト Api のサポートを提供します。 64 ビット PC 上の既定のディレクトリに、キットをインストールした場合の場所は。

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\JsProvider.d.ts`

VSCode での IntelliSense の定義ファイルを使用するには

1. 定義ファイルの JSProvider.d.ts

2. 定義ファイルをスクリプトと同じフォルダーにコピーします。

3. 追加`/// <reference path="JSProvider.d.ts" />`JavaScript スクリプト ファイルの先頭にします。

JavaScript ファイル内の参照を VS Code 自動的に表示されます IntelliSense ホストだけでなく、スクリプト内の構造体 JSProvider で提供される Api で。 たとえば、「ホスト」を入力します。 すべての利用可能なデバッガー モデル Api の IntelliSense が表示されます。


## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanjavascript-resources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>JavaScript リソース


JavaScript のデバッグ拡張機能を開発する際に役立つ可能性がある JavaScript リソースを次に示します。

-   [JavaScript コードの記述](https://docs.microsoft.com/scripting/javascript/writing-javascript-code)

-   [JScript 言語のツアー](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/t895bwkh(v=vs.100))

-   [Mozilla JavaScript リファレンス](https://developer.mozilla.org/docs/Web/JavaScript)

-   [WinJS:JavaScript 用 Windows ライブラリ](https://github.com/winjs/winjs)

-   [ECMAScript 6-新機能:比較 (&) の概要](https://es6-features.org/)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[JavaScript デバッガーの スクリプトの例](javascript-debugger-example-scripts.md)

[JavaScript の拡張機能のネイティブ オブジェクト](native-objects-in-javascript-extensions.md)











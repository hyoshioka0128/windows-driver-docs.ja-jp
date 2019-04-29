---
title: PLMDebug
description: PLMDebug.exe は、Windows デバッガーを使用して、プロセスのライフ サイクル管理 (PLM) を実行している Windows アプリをデバッグすることができるツールです。
ms.assetid: 68BE8F5D-6425-43E2-B5BC-C1D35614AB32
keywords:
- デバッグ PLMDebug Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PLMDebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fab398b359d46a8c2147c2d3d67994a236ee4f52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387935"
---
# <a name="plmdebug"></a>PLMDebug


PLMDebug.exe は、Windows デバッガーを使用して、プロセスのライフ サイクル管理 (PLM) を実行している Windows アプリをデバッグすることができるツールです。 PLMDebug、中断、再開、および Windows アプリを終了して手動で制御するができます。

**ヒント:**  Windows 10 バージョン 1607 以降では、UWP アプリをデバッグする .createpackageapp など、UWP のコマンドを使用することができます。 詳細については、次を参照してください。 [WinDbg を使用して UWP アプリのデバッグ](debugging-a-uwp-app-using-windbg.md)します。

 

**PLMDebug の入手先**

含まれている PLMDebug.exe[ツールを Windows のデバッグ](index.md)します。

```console
plmdebug /query [Package]
plmdebug /enableDebug Package [DebuggerCommandLine]
plmdebug /terminate Package
plmdebug /forceterminate Package
plmdebug /cleanterminate Package
plmdebug /suspend Package
plmdebug /resume Package
plmdebug /disableDebug Package
plmdebug /enumerateBgTasks Package
plmdebug /activateBgTaskTaskId
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Package"></span><span id="_______package"></span><span id="_______PACKAGE"></span> *パッケージ*  
パッケージまたは実行中のプロセスの ID の完全名。

<span id="_______DebuggerCommandLine"></span><span id="_______debuggercommandline"></span><span id="_______DEBUGGERCOMMANDLINE"></span> *DebuggerCommandLine*  
デバッガーを開くコマンドラインです。 コマンド ライン デバッガーへの完全パスを含める必要があります。 パスに空白がある場合は、引用符で囲む必要があります。 コマンドラインでは、引数を含めることもできます。 例をいくつか紹介します。

`"C:\Program Files (x86)\Windows Kits\8.0\Debuggers\x64\WinDbg.exe"`

`"\"C:\Program Files\Debugging Tools for Windows (x64)\WinDbg.exe\" -server npipe:pipe=test"`

<span id="________query_Package"></span><span id="________query_package"></span><span id="________QUERY_PACKAGE"></span> **/query** \[*Package*\]  
パッケージのインストールの実行中の状態を表示します。 場合*パッケージ*が指定されていない、このコマンドは、インストールされているすべてのパッケージの実行中の状態を表示します。

<span id="________enableDebug_Package_DebuggerCommandLine"></span><span id="________enabledebug_package_debuggercommandline"></span><span id="________ENABLEDEBUG_PACKAGE_DEBUGGERCOMMANDLINE"></span> **/enableDebug** *Package* \[*DebuggerCommandLine*\]  
パッケージのデバッグの参照カウントをインクリメントします。 0 以外のデバッグがある場合は、パッケージは PLM ポリシーから除外されて参照カウントします。 呼び出しごとに **/enableDebug**への呼び出しと組み合わせて使用する必要があります/**disableDebug**します。 指定した場合*DebuggerCommandLine*、パッケージからのすべてのアプリを起動するときに、デバッガーをアタッチします。

<span id="________terminate_Package"></span><span id="________terminate_package"></span><span id="________TERMINATE_PACKAGE"></span> **/terminate** *パッケージ*  
パッケージを終了します。

<span id="________forceTerminate_Package"></span><span id="________forceterminate_package"></span><span id="________FORCETERMINATE_PACKAGE"></span> **/forceTerminate** *パッケージ*  
パッケージの強制的に終了します。

<span id="________cleanTerminate_Package"></span><span id="________cleanterminate_package"></span><span id="________CLEANTERMINATE_PACKAGE"></span> **/cleanTerminate** *Package*  
中断し、パッケージを終了します。

<span id="________suspend_Package"></span><span id="________suspend_package"></span><span id="________SUSPEND_PACKAGE"></span> **/suspend** *Package*  
パッケージを中断します。

<span id="________resume_Package"></span><span id="________resume_package"></span><span id="________RESUME_PACKAGE"></span> **/再開***パッケージ*  
パッケージを再開します。

<span id="________disableDebug_Package"></span><span id="________disabledebug_package"></span><span id="________DISABLEDEBUG_PACKAGE"></span> **/disableDebug** *Package*  
パッケージのデバッグの参照カウントをデクリメントします。

<span id="________enumerateBgTasksPackage"></span><span id="________enumeratebgtaskspackage"></span><span id="________ENUMERATEBGTASKSPACKAGE"></span> **/enumerateBgTasks * * * パッケージ*  
パッケージのバック グラウンド タスクの id を列挙します。

<span id="________activateBgTaskTaskId"></span><span id="________activatebgtasktaskid"></span><span id="________ACTIVATEBGTASKTASKID"></span> **/activateBgTask***TaskId*  
バック グラウンド タスクをアクティブにします。 PLMDebug を使用してすべてのバック グラウンド タスクをアクティブにできることに注意してください。

<a name="remarks"></a>注釈
-------

呼び出す必要があります**plmdebug/enableDebug**中断のいずれかを呼び出す前に、再開、または関数を終了します。

メソッドを呼び出して、PLMDebug ツール、 [IPackageDebugSettings インターフェイス](https://go.microsoft.com/fwlink/p/?LinkID=267918)します。 このインターフェイスでは、手動プロセスのライフ サイクル管理、アプリを制御することができます。 このインターフェイスを通じて、その結果、このツールを使用) は、中断して再開、および Windows アプリを終了できます。 注意のメソッド、 [IPackageDebugSettings インターフェイス](https://go.microsoft.com/fwlink/p/?LinkID=267918)パッケージ全体に適用されます。 中断、再開、および、パッケージでアプリを実行中のすべてに影響を終了します。

<a name="examples"></a>例
--------

**例 1**

**アプリを起動するときにデバッガーをアタッチします。**

MyApp という名前のパッケージでは MyApp という名前のアプリがあるとします\_1.0.0.0\_x64\_\_tnq5r49etfg3c します。 完全な名前を表示して、インストールされているすべてのパッケージの状態を実行して、パッケージがインストールされていることを確認します。 コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**plmdebug /query**

```console
Package full name: 1daa103b-74e1-426d-8193-b6bc7ed66fed_1.0.0.0_x86__tnq5r49etfg3c
Package state: Terminated

Package full name: 41fb5f27-7b60-4f5e-8459-803673131dd9_1.0.0.0_x86__tnq5r49etfg3c
Package state: Suspended
...
Package full name: MyApp_1.0.0.0_x64__tnq5r49etfg3c
Package state: Terminated
...
```

パッケージのデバッグの参照カウントをインクリメントし、WinDbg をアプリが起動するときにアタッチすることを指定します。

**plmdebug /enableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c "C:\\Program Files (x86)\\Windows Kits\\8.0\\Debuggers\\x64\\WinDbg.exe"**

アプリを起動するときに、WinDbg はアタッチし、分割します。

デバッグが完了したら、デバッガーをデタッチします。 パッケージのデバッグの参照カウントをデクリメントします。

**plmdebug/disableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

**例 2**

**既に実行されているアプリにデバッガーをアタッチします。**

既に実行中の MyApp に WinDbg をアタッチするとします。 WinDbg での**ファイル**] メニューの [選択**プロセスにアタッチする**します。 MyApp のプロセス ID に注意してください。 たとえば、プロセス ID が 4816 とします。

MyApp を含むパッケージのデバッグの参照カウントをインクリメントします。

**plmdebug/enableDebug 4816**

、WinDbg で、**プロセスにアタッチ** ダイアログ ボックスでは、プロセス 4816、を選択し、クリックして**OK**します。 WinDbg は、MyApp に接続されます。

MyApp のデバッグが完了したら、デバッガーをデタッチします。 パッケージのデバッグの参照カウントをデクリメントします。

**plmdebug /disableDebug 4816**

**例 3**

**手動で中断し、アプリの再開**

手動で中断し、アプリを再開するとします。 最初に、アプリを含むパッケージのデバッグの参照カウントをインクリメントします。

**plmdebug/enableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

パッケージを中断します。 アプリの中断ハンドラーが呼び出され、これは、デバッグに役立ちます。

**plmdebug MyApp の中断/\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

デバッグが完了したら、パッケージを再開します。

**plmdebug/resume MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

最後に、パッケージのデバッグの参照カウントをデクリメントします。

**plmdebug/disableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[トリガーする方法を中断、再開、およびバック グラウンド イベントを Windows アプリ](https://go.microsoft.com/fwlink/p/?LinkID=267916)

[Windows 用デバッグ ツールに含まれるツール](extra-tools.md)

 

 







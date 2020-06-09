---
title: PLMDebug
description: PLMDebug は、Windows デバッガーを使用して、プロセスライフサイクル管理 (PLM) で実行される Windows アプリをデバッグできるツールです。
ms.assetid: 68BE8F5D-6425-43E2-B5BC-C1D35614AB32
keywords:
- PLMDebug Windows のデバッグ
ms.date: 06/03/2020
topic_type:
- apiref
api_name:
- PLMDebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd4f8f2fcd1eab3ec3105890e1580a3d0234449e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534437"
---
# <a name="plmdebug"></a>PLMDebug

PLMDebug は、Windows デバッガーを使用して、プロセスライフサイクル管理 (PLM) で実行される Windows アプリをデバッグできるツールです。 PLMDebug を使用すると、Windows アプリの中断、再開、および終了を手動で制御できます。

**ヒント**   Windows 10 バージョン1607以降では、createpackageapp などの UWP コマンドを使用して UWP アプリをデバッグできます。 詳細については[、「WinDbg を使用した UWP アプリのデバッグ](debugging-a-uwp-app-using-windbg.md)」を参照してください。

**PLMDebug を取得する場所**

PLMDebug は、 [Windows 用のデバッグツール](index.md)に含まれています。

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
plmdebug /activateBgTaskTaskId "{TaskID}"
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ

<span id="_______Package"></span><span id="_______package"></span><span id="_______PACKAGE"></span>*パッケージ*  
パッケージの完全な名前、または実行中のプロセスの ID。

<span id="_______DebuggerCommandLine"></span><span id="_______debuggercommandline"></span><span id="_______DEBUGGERCOMMANDLINE"></span>*デバッガーのコマンドライン*  
デバッガーを開くためのコマンドライン。 コマンドラインには、デバッガーへの完全パスが含まれている必要があります。 パスに空白が含まれている場合は、引用符で囲む必要があります。 コマンドラインに引数を含めることもできます。 次に例をいくつか示します。

`"C:\Program Files (x86)\Windows Kits\8.0\Debuggers\x64\WinDbg.exe"`

`"\"C:\Program Files\Debugging Tools for Windows (x64)\WinDbg.exe\" -server npipe:pipe=test"`

<span id="________query_Package"></span><span id="________query_package"></span><span id="________QUERY_PACKAGE"></span>**/query** \[*パッケージ*\]  
インストールされているパッケージの実行状態を表示します。 *Package*が指定されていない場合、このコマンドは、インストールされているすべてのパッケージの実行状態を表示します。

<span id="________enableDebug_Package_DebuggerCommandLine"></span><span id="________enabledebug_package_debuggercommandline"></span><span id="________ENABLEDEBUG_PACKAGE_DEBUGGERCOMMANDLINE"></span>**/enabledebug** *パッケージ* \[ *デバッガーコマンドライン*\]  
パッケージのデバッグ参照カウントをインクリメントします。 デバッグ参照カウントが0以外の場合、パッケージは PLM ポリシーから除外されます。 / **Enabledebug**の各呼び出しは、/**disabledebug**の呼び出しと組み合わせて使用する必要があります。 デバッガーの*コマンドライン*を指定すると、パッケージからアプリを起動するときにデバッガーがアタッチされます。

<span id="________terminate_Package"></span><span id="________terminate_package"></span><span id="________TERMINATE_PACKAGE"></span>**/終了***パッケージ*  
パッケージを終了します。

<span id="________forceTerminate_Package"></span><span id="________forceterminate_package"></span><span id="________FORCETERMINATE_PACKAGE"></span>**/ForceTerminate** *パッケージ*  
パッケージを強制的に終了します。

<span id="________cleanTerminate_Package"></span><span id="________cleanterminate_package"></span><span id="________CLEANTERMINATE_PACKAGE"></span>**/CleanTerminate** *パッケージ*  
パッケージを中断してから終了します。

<span id="________suspend_Package"></span><span id="________suspend_package"></span><span id="________SUSPEND_PACKAGE"></span>**/中断***パッケージ*  
パッケージを中断します。

<span id="________resume_Package"></span><span id="________resume_package"></span><span id="________RESUME_PACKAGE"></span>**/resume** *パッケージ*の再開 (_r)  
パッケージを再開します。

<span id="________disableDebug_Package"></span><span id="________disabledebug_package"></span><span id="________DISABLEDEBUG_PACKAGE"></span>**/disabledebug** *パッケージ*  
パッケージのデバッグ参照カウントをデクリメントします。

<span id="________enumerateBgTasksPackage"></span><span id="________enumeratebgtaskspackage"></span><span id="________ENUMERATEBGTASKSPACKAGE"></span>**/EnumerateBgTasks** *パッケージ*  
パッケージのバックグラウンドタスク id を列挙します。

<span id="________activateBgTaskTaskId"></span><span id="________activatebgtasktaskid"></span><span id="________ACTIVATEBGTASKTASKID"></span>**/activateBgTask**"{*TaskId*}"  
バックグラウンドタスクをアクティブにします。 PLMDebug を使用してすべてのバックグラウンドタスクをアクティブにできるわけではないことに注意してください。 TaskID は、中かっこと引用符で囲む必要があります。 次に例を示します。

`plmdebug.exe /activatebgtask "{29421c11-1e1a-47a4-9121-949ce9e25456}"`

<a name="remarks"></a>解説
-------

中断、再開、または終了の各関数を呼び出す前に、 **plmdebug/enabledebug**を呼び出す必要があります。

PLMDebug ツールは、 [Ipackagedebugsettings インターフェイス](https://docs.microsoft.com/windows/win32/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)のメソッドを呼び出します。 このインターフェイスを使用すると、アプリのプロセスライフサイクル管理を手動で制御できます。 このインターフェイスを使用して、Windows アプリを中断、再開、および終了することができます (その結果、このツールを使用します)。 [Ipackagedebugsettings インターフェイス](https://docs.microsoft.com/windows/win32/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)のメソッドは、パッケージ全体に適用されることに注意してください。 中断、再開、および終了は、パッケージ内で現在実行中のすべてのアプリに影響します。

<a name="examples"></a>例
--------

**例 1**

**アプリが起動されたときにデバッガーをアタッチする**

Myapp という名前のアプリがあるとします。これは、MyApp 1.0.0.0 x64 tnq5r49etfg3c という名前のパッケージに含まれてい \_ \_ \_ \_ ます。 完全な名前を表示し、インストールされているすべてのパッケージを実行して、パッケージがインストールされていることを確認します。 コマンドプロンプトウィンドウで、次のコマンドを入力します。

**plmdebug/query**

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

パッケージのデバッグ参照カウントをインクリメントし、アプリの起動時に WinDbg をアタッチするように指定します。

**plmdebug/enabledebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c "C: \\ Program Files (x86) \\ Windows kit \\ 8.0 \\ デバッガー \\ x64 \\ WinDbg .exe"**

アプリを起動すると、WinDbg がアタッチされ、中断されます。

デバッグが完了したら、デバッガーをデタッチします。 次に、パッケージのデバッグ参照カウントをデクリメントします。

**plmdebug/disabledebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

**例 2**

**既に実行中のアプリにデバッガーをアタッチする**

既に実行されているである、MyApp に WinDbg をアタッチするとします。 [WinDbg] の [**ファイル**] メニューで、[**プロセスにアタッチ**] を選択します。 MyApp のプロセス ID をメモしておきます。 たとえば、プロセス ID が4816であるとします。

MyApp を含むパッケージのデバッグ参照カウントをインクリメントします。

**plmdebug/enabledebug 4816**

[WinDbg] の [**プロセスにアタッチ**] ダイアログボックスで、[プロセス 4816] を選択し、[ **OK**] をクリックします。 WinDbg が MyApp にアタッチされます。

MyApp のデバッグが終了したら、デバッガーをデタッチします。 次に、パッケージのデバッグ参照カウントをデクリメントします。

**plmdebug/disabledebug 4816**

**例 3**

**アプリを手動で中断して再開する**

アプリを手動で中断して再開するとします。 最初に、アプリを含むパッケージのデバッグ参照カウントをインクリメントします。

**plmdebug/enabledebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

パッケージを中断します。 アプリの中断ハンドラーが呼び出されます。これはデバッグに役立ちます。

**plmdebug/suspend MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

デバッグが完了したら、パッケージを再開します。

**plmdebug/resume MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

最後に、パッケージのデバッグ参照カウントをデクリメントします。

**plmdebug/disabledebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

**例 4**

**バックグラウンドタスクを手動でアクティブ化する**

デバッグ用にバックグラウンドタスクを手動でアクティブ化するには、登録されているバックグラウンドタスクの一覧を照会して、plmdebug でアクティブ化することができます。

最初に、登録されたバックグラウンドタスクのセットを照会します。

**plmdebug/enumeratebgtasks MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**
```console
Package full name is MyApp_1.0.0.0_x64__tnq5r49etfg3c.
Background Tasks:
SampleTask : {50DB0363-D722-4E23-A18F-1EF49B226CC3}
```

タスクがアクティブになることを保証するには、まずデバッグモードを有効にします。 たとえば、TimeTrigger によってアクティブ化されたタスクのような便宜的なタスクは、システムがバッテリセーバーにある間はアクティブになりません。 パッケージでデバッグモードを有効にすると、アクティブ化を妨げるポリシーがシステムによって無視されます。

**plmdebug/enabledebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

次に、列挙した登録 GUID を使用して、目的のタスクをアクティブ化します。

**plmdebug/activatebgtask "{50DB0363-D722-4E23-A18F-1EF49B226CC3}"**

## <a name="see-also"></a>こちらもご覧ください

[Visual Studio で UWP アプリをデバッグするときに、中断、再開、およびバックグラウンド イベントをトリガーする方法](https://docs.microsoft.com/visualstudio/debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio)

[Debugging Tools for Windows に含まれるツール](extra-tools.md)

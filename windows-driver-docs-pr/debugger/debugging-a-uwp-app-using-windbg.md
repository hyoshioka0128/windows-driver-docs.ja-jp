---
title: WinDbg を使用して UWP アプリのデバッグ
description: WinDbg を使用してユニバーサル Windows プラットフォーム (UWP) アプリをデバッグすることができます。
ms.assetid: 1CE337AC-54C0-4EF5-A374-3ECF1D72BA60
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e3ffdbbde7fd0177e3ab5707f1be90e887d1a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559910"
---
# <a name="debugging-a-uwp-app-using-windbg"></a>WinDbg を使用して UWP アプリのデバッグ


WinDbg を使用してユニバーサル Windows プラットフォーム (UWP) アプリをデバッグすることができます。 このアプローチは通常使用の高度なシナリオは、場所、ビルドを使用して Visual Studio デバッガーでデバッグ タスクを完了することはできません。 Visual Studio でのデバッグの詳細については、[Visual Studio でのデバッグ](https://msdn.microsoft.com/library/sc65sadd.aspx)を参照してください。

## <a name="span-idattachingtoauwpappspanspan-idattachingtoauwpappspanspan-idattachingtoauwpappspanattaching-to-a-uwp-app"></a><span id="Attaching_to_a_UWP_app"></span><span id="attaching_to_a_uwp_app"></span><span id="ATTACHING_TO_A_UWP_APP"></span>UWP アプリへのアタッチ


UWP のプロセスにアタッチすると、ユーザー モード プロセスにアタッチする場合と同じです。 たとえば、WinDbg で割り当てることができます、実行中のプロセスを選択して**ファイルからプロセスにアタッチ**メニューまたは F6 キーを押しています。 詳細については、[デバッグ ユーザー モード プロセスを使用して WinDbg](debugging-a-user-mode-process-using-windbg.md)を参照してください。

UWP アプリは、デバッグ中でない場合と同じ方法では中断されません。 明示的に中断または再開するため、UWP アプリを .suspendpackage と .resumepackage コマンド (以下の詳細) を使用できます。 プロセスのライフ サイクル管理 (PLM) UWP アプリで使用される一般的な情報は、[アプリのライフ サイクル](https://msdn.microsoft.com/library/windows/apps/mt243287)と[Launching, resuming, とバック グラウンド タスク](https://msdn.microsoft.com/library/windows/apps/mt227652)を参照してください。

## <a name="span-idlaunchinganddebuggingauwpappspanspan-idlaunchinganddebuggingauwpappspanspan-idlaunchinganddebuggingauwpappspanlaunching-and-debugging-a-uwp-app"></a><span id="Launching_and_debugging__a_UWP_app"></span><span id="launching_and_debugging__a_uwp_app"></span><span id="LAUNCHING_AND_DEBUGGING__A_UWP_APP"></span>起動して、UWP アプリのデバッグ


PlmPackage - と - plmApp コマンド ライン パラメーターは、デバッガー下でアプリを起動するデバッガーに指示します。

```console
windbg.exe -plmPackage <PLMPackageName> -plmApp <ApplicationId> [<parameters>]
```

1 つのパッケージ内に複数のアプリを含まれていることができますので両方&lt;PLMPackage&gt;と&lt;ApplicationId&gt;パラメーターが必要です。 これは、パラメーターの概要を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>パラメーター</strong></td>
<td align="left"><strong>説明</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left">アプリケーション パッケージの名前。 すべての UWP アプリケーションの一覧に、.querypackages コマンドを使用します。 パッケージの場所へのパスを指定ではなくパッケージ名だけを指定します。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>ApplicationId は、アプリケーション マニフェスト ファイルにあるし、このトピックで説明したように、.querypackage または .querypackages コマンドを使用して表示できます。</p>
<p>アプリケーション マニフェスト ファイルの詳細については、<a href="https://msdn.microsoft.com/library/windows/apps/br211474" data-raw-source="[App package manifest](https://msdn.microsoft.com/library/windows/apps/br211474)">アプリ パッケージのマニフェスト</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;パラメーター&gt;]</td>
<td align="left"><p>省略可能なパラメーターは、アプリに渡されます。 すべてのアプリまたは使用して、パラメーターが必要です。</p></td>
</tr>
</tbody>
</table>

 

**HelloWorld サンプル**

UWP のデバッグを示すためには、このトピックは「HelloWorld サンプルを使用して[作成"Hello, world"アプリ (XAML)](https://msdn.microsoft.com/windows/uwp/get-started/create-a-hello-world-app-xaml-universal)します。

テストの実行可能なアプリを作成するには、まで、ラボの 3 つの手順を完了する必要はのみです。

**AppId とパッケージの完全な名前を検索します。**

完全なパッケージ名と、アプリ Id を検索するのにには、.querypackages コマンドを使用します。 .Querypackages しユーザー CRTL + F、HelloWorld など、アプリケーション名の出力で上へ検索 を入力します。 エントリは、CTRL キーを押しながら F キーを使用して配置が、表示されます、パッケージ フル_ネーム、たとえば*e24caf14-8483-4743-b80c-ca46c28c75df\_1.0.0.0\_x86\_\_97ghe447vaan8*とAppId*アプリ*します。

以下に例を示します。

```dbgcmd
0:000>  .querypackages 
...
Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Unknown
AppId: App
...
```

**基本パッケージの名前を表示する、マニフェストに**

トラブルシューティングについては、Visual Studio で、基本パッケージの名前を表示します。

Visual Studio で、基本パッケージ名を検索するには、プロジェクト エクスプ ローラーで、ApplicationManifest.xml ファイルをクリックします。 基本パッケージの名前は"Package name"としてパッケージ化 タブで表示されます。 既定では、パッケージ名になります、GUID では、たとえば*e24caf14-8483-4743-b80c-ca46c28c75df*します。

メモ帳を使用して、基本パッケージの名前を検索する、ApplicationManifest.xml ファイルを開くし、検索、 **Id 名**タグ。

```xml
  <Identity
    Name="e24caf14-8483-4743-b80c-ca46c28c75df"
    Publisher="CN= User1"
    Version="1.0.0.0" />
```

**マニフェストに、アプリケーション Id を検索します。**

インストールされている UWP アプリのマニフェスト ファイルでアプリケーション Id を検索する検索、*アプリケーション Id*エントリ。

たとえば、hello world アプリのアプリケーション ID は*アプリ*します。

```xml
<Application Id="App"
      Executable="$targetnametoken$.exe"
      EntryPoint="HelloWorld.App">
```

**WinDbg のコマンドラインの例**

これは、読み込み、完全なパッケージ名とアプリ Id を使用して、デバッガー下で HelloWorld アプリケーション コマンドラインの例です。

```console
windbg.exe -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

## <a name="span-idlaunchingabackgroundtaskunderthedebuggerspanspan-idlaunchingabackgroundtaskunderthedebuggerspanspan-idlaunchingabackgroundtaskunderthedebuggerspanlaunching-a-background-task-under-the-debugger"></a><span id="Launching_a_background_task_under_the_debugger"></span><span id="launching_a_background_task_under_the_debugger"></span><span id="LAUNCHING_A_BACKGROUND_TASK_UNDER_THE_DEBUGGER"></span>デバッガーの下でバック グラウンド タスクの開始


TaskId を使用してコマンドラインからデバッガーの下でバック グラウンド タスクを明示的に起動できます。 これを行うには、plmPackage - と - plmBgTaskId コマンド ライン パラメーターを使用します。

```console
windbg.exe -plmPackage <PLMPackageName> -plmBgTaskId <BackgroundTaskId>
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>パラメーター</strong></td>
<td align="left"><strong>説明</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left"><p>アプリケーション パッケージの名前。 すべての UWP アプリケーションの一覧に、.querypackages コマンドを使用します。 パッケージの場所へのパスを指定ではなくパッケージ名だけを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left">&lt;BackgroundTaskId&gt;</td>
<td align="left"><p>BackgroundTaskId を以下に示すように、.querypackages コマンドを使用して配置できます。</p>
<p>アプリケーション マニフェスト ファイルの詳細については、<a href="https://msdn.microsoft.com/library/windows/apps/br211474" data-raw-source="[App package manifest](https://msdn.microsoft.com/library/windows/apps/br211474)">アプリ パッケージのマニフェスト</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

これは、デバッガーの下で SDKSamples.BackgroundTask コードの読み込みの例です。

```console
windbg.exe -plmPackage Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe -plmBgTaskId {ee4438ee-22db-4cdd-85e4-8ad8a1063523}
```

UWP のデバッグに精通するバック グラウンド タスクのサンプル コードを実験できます。 ダウンロード[バック グラウンド タスクのサンプル](https://code.msdn.microsoft.com/windowsapps/Background-Task-Sample-9209ade9)します。

BackgroundTaskId を検索するのにには、.querypackages コマンドを使用します。 CTRL + F を使用して、アプリを検索し、*バック グラウンド タスク Id*フィールド。 タスク id と関連付けられているバック グラウンド タスクの名前を表示するバック グラウンド タスクを実行する必要があります。

```dbgcmd
0:000> .querypackages
...
Package Full Name: Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x86__8wekyb3d8bbwe
Package Display Name: BackgroundTask C++ sample
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
Publisher Display Name: Microsoft Corporation
Install Folder: C:\Users\user1\Documents\Visual Studio 2015\Projects\Background_task_sample\C++\Debug\BackgroundTask.Windows\AppX
Package State: Running
AppId: BackgroundTask.App
Background Task Name: SampleBackgroundTask
Background Task Id: {ee4438ee-22db-4cdd-85e4-8ad8a1063523}
...
```

表示する .querypackage を使用するには、完全なパッケージ名がわかっている場合、*バック グラウンド タスク Id*フィールド。

PLMDebug の enumerateBgTasks オプションを使用して、BackgroundTaskId を検索することもできます。 PMLDebug utiltity の詳細については、[ **PLMDebug**](plmdebug.md)を参照してください。

```console
C:\Program Files\Debugging Tools for Windows (x64)>PLMDebug /enumerateBgTasks Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe
Package full name is Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe.
Background Tasks:
SampleBackgroundTask : {C05806B1-9647-4765-9A0F-97182CEA5AAD}

SUCCEEDED
```

## <a name="span-iddebuggingauwpprocessremotelyusingaprocessserverdbgsrvspanspan-iddebuggingauwpprocessremotelyusingaprocessserverdbgsrvspanspan-iddebuggingauwpprocessremotelyusingaprocessserverdbgsrvspandebugging-a-uwp-process-remotely-using-a-process-server-dbgsrv"></a><span id="Debugging_a_UWP_process_remotely_using_a_Process_Server__DbgSrv_"></span><span id="debugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_"></span><span id="DEBUGGING_A_UWP_PROCESS_REMOTELY_USING_A_PROCESS_SERVER__DBGSRV_"></span>プロセス サーバー (DbgSrv) を使用してリモートでの UWP プロセスのデバッグ


すべての plm の\*dbgsrv でコマンドが正常に動作します。 Dbgsrv を使用してデバッグするには、使用に premote スイッチ dbgsrv の接続文字列に置き換えます。

```console
windbg.exe -premote npipe:pipe=fdsa,server=localhost -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

詳細については、- premote のオプションの詳細についてを参照してください[プロセス サーバー (ユーザー モード)](process-servers--user-mode-.md)と[プロセス サーバーの例](process-server-examples.md)します。

## <a name="span-idsummaryofuwpappcommandsspanspan-idsummaryofuwpappcommandsspanspan-idsummaryofuwpappcommandsspansummary-of-uwp-app-commands"></a><span id="Summary_of_UWP_app_commands"></span><span id="summary_of_uwp_app_commands"></span><span id="SUMMARY_OF_UWP_APP_COMMANDS"></span>UWP アプリ コマンドの概要


このセクションでは、UWP アプリのデバッガー コマンドの概要を提供します。

**パッケージ情報の収集**

**.querypackage**

.Querypackage では、UWP アプリケーションの状態が表示されます。 たとえば、アプリが実行されている場合ことができますで、 *Active*状態。

```dbgcmd
.querypackage <PLMPackageName>
```

以下に例を示します。

```dbgcmd
0:000> .querypackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Running
AppId: App
Executable: HelloWorld.exe
```

**.querypackages**

.Querypackages コマンドには、インストールされているすべての UWP アプリケーションとその現在の状態が一覧表示します。

```dbgcmd
.querypackages
```

以下に例を示します。

```dbgcmd
0:000> .querypackages
...
Package Full Name: Microsoft.MicrosoftSolitaireCollection_3.9.5250.0_x64__8wekyb3d8bbwe
Package Display Name: Microsoft Solitaire Collection
Version: 3.9.5250.0
Processor Architecture: x64
Publisher: CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
Publisher Display Name: Microsoft Studios
Install Folder: C:\Program Files\WindowsApps\Microsoft.MicrosoftSolitaireCollection_3.9.5250.0_x64__8wekyb3d8bbwe
Package State: Unknown
AppId: App

Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Running
AppId: App
Executable: HelloWorld.exe

Package Full Name: Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x86__8wekyb3d8bbwe
Package Display Name: BackgroundTask C++ sample
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
Publisher Display Name: Microsoft Corporation
Install Folder: C:\Users\user1\Documents\Visual Studio 2015\Projects\Background_task_sample\C++\Debug\BackgroundTask.Windows\AppX
Package State: Unknown
AppId: BackgroundTask.App

...
```

**デバッグ用のアプリを起動します。**

**.createpackageapp**

.Createpackageapp コマンドでは、デバッグを有効にし、UWP アプリケーションを起動します。

```dbgcmd
.createpackageapp <PLMPackageName> <ApplicationId> [<parameters>] 
```

このテーブルは、.createpackageapp のパラメーターを一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>パラメーター</strong></td>
<td align="left"><strong>説明</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left">アプリケーション パッケージの名前。 すべての UWP アプリケーションの一覧に、.querypackages コマンドを使用します。 パッケージの場所へのパスを指定ではなくパッケージ名だけを指定します。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>ApplicationId は、このトピックで前述したように、.querypackage または .querypackages を使用して配置できます。</p>
<p>アプリケーション マニフェスト ファイルの詳細については、<a href="https://msdn.microsoft.com/library/windows/apps/br211474" data-raw-source="[App package manifest](https://msdn.microsoft.com/library/windows/apps/br211474)">アプリ パッケージのマニフェスト</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;パラメーター&gt;]</td>
<td align="left">アプリケーションに渡される省略可能なパラメーター。 すべてのアプリケーションが必要ですか、これらの省略可能なパラメーターを使用します。</td>
</tr>
</tbody>
</table>

 

以下に例を示します。

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

**コマンドのデバッグを有効にしての使用を無効化**

**.enablepackagedebug**

.Enablepackagedebug コマンドは、UWP アプリケーションのデバッグを有効にします。 .Enablepackagedebug を使用する必要があります、中断のいずれかを呼び出す前に、再開、または関数を終了します。

.Createpackageapp コマンドは、アプリのデバッグをまた有効に注意してください。

```dbgcmd
.enablepackagedebug <PLMPackageName>
```

以下に例を示します。

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.disablepackagedebug**

.Disablepackagedebug コマンドでは、UWP アプリケーションのデバッグを無効にします。

```dbgcmd
.disablepackagedebug <PLMPackageName>
```

以下に例を示します。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**開始して、アプリを停止しています**

中断、メモは、再開、および、パッケージ アプリの実行中のすべてに影響を終了します。

**.suspendpackage**

.Suspendpackage のコマンドは、UWP アプリケーションを中断します。

```dbgcmd
.suspendpackage <PLMPackageName> 
```

以下に例を示します。

```dbgcmd
0:024> .suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.resumepackage**

.Resumepackage コマンドは、UWP アプリケーションを再開します。

```dbgcmd
.resumepackage <PLMPackageName> 
```

以下に例を示します。

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.terminatepackageapp**

.Terminatepackageapp コマンドでは、すべてのパッケージの UWP アプリケーションが終了します。

```dbgcmd
.terminatepackageapp <PLMPackageName> 
```

以下に例を示します。

```dbgcmd
.terminatepackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**バック グラウンド タスク**

**.activatepackagebgtask**

.Activatepackagebgtask コマンドでは、デバッグを有効にし、UWP のバック グラウンド タスクを起動します。

```dbgcmd
 .activatepackagebgtask <PLMPackageName> <bgTaskId>
```

以下に例を示します。

```dbgcmd
.activatepackagebgtask Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe {C05806B1-9647-4765-9A0F-97182CEA5AAD}
```

## <a name="span-idusageexamplesspanspan-idusageexamplesspanspan-idusageexamplesspanusage-examples"></a><span id="Usage_Examples"></span><span id="usage_examples"></span><span id="USAGE_EXAMPLES"></span>使用例


**アプリを起動するときにデバッガーをアタッチします。**

E24caf14-8483-4743-b80c-ca46c28c75df という名前のパッケージでは、HelloWorld という名前のアプリがあるとします\_1.0.0.0\_x86\_\_97ghe447vaan8 します。 完全な名前を表示して、インストールされているすべてのパッケージの状態を実行して、パッケージがインストールされていることを確認します。 コマンド プロンプト ウィンドウで、次のコマンドを入力します。 CTRL + F を使用すると、アプリ名の HelloWorld コマンドの出力を検索します。

```dbgcmd
.querypackages 
...

Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Unknown
AppId: App

...
```

起動し、アプリにアタッチするには、.createpackageapp を使用します。 .Createpackageapp コマンドは、アプリのデバッグもできます。

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

デバッグが完了したら、.disablepackagedebug コマンドを使用して、パッケージのデバッグの参照カウントをデクリメントします。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**既に実行されているアプリにデバッガーをアタッチします。**

既に実行中の MyApp に WinDbg をアタッチするとします。 WinDbg での**ファイル**] メニューの [選択**プロセスにアタッチする**します。 MyApp のプロセス ID に注意してください。 たとえば、プロセス ID が 4816 とします。 MyApp を含むパッケージのデバッグの参照カウントをインクリメントします。

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

WinDbg での**プロセスにアタッチ** ダイアログ ボックスでは、プロセス 4816 を選択し、ok をクリックします。 WinDbg は、MyApp に接続されます。

デバッグが完了したら、.disablepackagedebug コマンドを使用して、パッケージのデバッグの参照カウントをデクリメントします。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**手動で中断し、アプリの再開**

手動で中断し、アプリを再開するこれらの手順に従います。 最初に、アプリを含むパッケージのデバッグの参照カウントをインクリメントします。

```dbgcmd
.enablepackagedebug  e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

パッケージを中断します。 アプリの中断ハンドラーが呼び出され、これは、デバッグに役立ちます。

```dbgcmd
.suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

デバッグが完了したら、パッケージを再開します。

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

最後に、パッケージのデバッグの参照カウントをデクリメントします。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WinDbg を使用したデバッグ](debugging-using-windbg.md)

 

 







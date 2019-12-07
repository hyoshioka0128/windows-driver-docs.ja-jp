---
title: WinDbg を使用した UWP アプリのデバッグ
description: WinDbg を使用してユニバーサル Windows プラットフォーム (UWP) アプリをデバッグできます。
ms.assetid: 1CE337AC-54C0-4EF5-A374-3ECF1D72BA60
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e38cf99e7c9a7159b6cb82b225468fad776c4ece
ms.sourcegitcommit: 9ebed9a7909b0e39a0efb1c23a5435bf36688d05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74898497"
---
# <a name="debugging-a-uwp-app-using-windbg"></a>WinDbg を使用した UWP アプリのデバッグ


WinDbg を使用してユニバーサル Windows プラットフォーム (UWP) アプリをデバッグできます。 この方法は、通常、組み込みの Visual Studio デバッガーを使用してデバッグタスクを完了できない高度なシナリオに使用されます。 Visual Studio でのデバッグの詳細については、「 [Visual studio でのデバッグ](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio?view=vs-2015)」を参照してください。

## <a name="span-idattaching_to_a_uwp_appspanspan-idattaching_to_a_uwp_appspanspan-idattaching_to_a_uwp_appspanattaching-to-a-uwp-app"></a><span id="Attaching_to_a_UWP_app"></span><span id="attaching_to_a_uwp_app"></span><span id="ATTACHING_TO_A_UWP_APP"></span>UWP アプリへのアタッチ


UWP プロセスへのアタッチは、ユーザーモードプロセスへのアタッチと同じです。 たとえば、WinDbg では、[ファイル] メニュー**の [プロセスにアタッチ**] をクリックするか、F6 キーを押して、実行中のプロセスにアタッチできます。 詳細については、「 [WinDbg を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-windbg.md)」を参照してください。

UWP アプリは、デバッグされていない場合と同じ方法で中断されることはありません。 UWP アプリを明示的に中断/再開するには、. suspendpackage および resumepackage コマンド (以下の詳細) を使用できます。 UWP アプリで使用されるプロセスライフサイクル管理 (PLM) に関する一般的な情報については、「[アプリのライフサイクル](https://docs.microsoft.com/windows/uwp/launch-resume/app-lifecycle)」と「[起動、再開、およびバックグラウンドタスク](https://docs.microsoft.com/windows/uwp/launch-resume/index)」を参照してください。

## <a name="span-idlaunching_and_debugging__a_uwp_appspanspan-idlaunching_and_debugging__a_uwp_appspanspan-idlaunching_and_debugging__a_uwp_appspanlaunching-and-debugging-a-uwp-app"></a><span id="Launching_and_debugging__a_UWP_app"></span><span id="launching_and_debugging__a_uwp_app"></span><span id="LAUNCHING_AND_DEBUGGING__A_UWP_APP"></span>UWP アプリの起動とデバッグ


-PlmPackage コマンドラインパラメーターと-Plmpackage コマンドラインパラメーターは、デバッガーでアプリを起動するように指示します。

```console
windbg.exe -plmPackage <PLMPackageName> -plmApp <ApplicationId> [<parameters>]
```

1つのパッケージ内に複数のアプリを含めることができるため、&lt;PLMPackage&gt; と &lt;ApplicationId&gt; パラメーターの両方が必要です。 これは、パラメーターの概要です。

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
<td align="left">アプリケーションパッケージの名前。 Querypackages コマンドを使用して、すべての UWP アプリケーションを一覧表示します。 パッケージの場所へのパスを指定せずに、パッケージ名だけを指定してください。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>ApplicationId はアプリケーションマニフェストファイルに格納されており、このトピックで説明されているように、querypackage または querypackages コマンドを使用して表示できます。</p>
<p>アプリケーションマニフェストファイルの詳細については、「アプリケーション<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">パッケージマニフェスト</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;パラメーター&gt;]</td>
<td align="left"><p>アプリに渡される省略可能なパラメーター。 すべてのアプリでパラメーターを使用したり、要求したりすることはできません。</p></td>
</tr>
</tbody>
</table>

 

**HelloWorld サンプル**

UWP のデバッグを示すために、このトピックでは、 [「Hello, world "アプリの作成 (XAML)](https://docs.microsoft.com/windows/uwp/get-started/create-a-hello-world-app-xaml-universal)」で説明されている HelloWorld の例を使用します。

実行可能なテストアプリを作成するには、ラボの手順 3. まで完了するだけで済みます。

**完全なパッケージ名と AppId の検索**

Querypackages コマンドを使用して、完全なパッケージ名と AppId を検索します。 「Querypackages」と入力します。次に、HelloWorld などのアプリケーション名の出力を検索します。 CTRL + F キーを使用してエントリを配置すると、パッケージの完全な名前が表示されます。たとえば、 *e24caf14-8483-4743-b80c-ca46c28c75df\_1.0.0.0\_x86\_\_97ghe447vaan8* 、*アプリ*の AppId などです。

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

**マニフェスト内のでの基本パッケージ名の表示**

トラブルシューティングのために、Visual Studio で基本パッケージ名を表示することができます。

Visual Studio で基本パッケージ名を検索するには、プロジェクトエクスプローラーで ApplicationManifest .xml ファイルをクリックします。 基本パッケージ名は、[パッケージ化] タブの下に "パッケージ名" として表示されます。 既定では、パッケージ名は*e24caf14-8483-4743-b80c-ca46c28c75df*などの GUID になります。

メモ帳を使用して基本パッケージ名を検索するには、ApplicationManifest .xml ファイルを開き、 **Identity name**タグを見つけます。

```xml
  <Identity
    Name="e24caf14-8483-4743-b80c-ca46c28c75df"
    Publisher="CN= User1"
    Version="1.0.0.0" />
```

**マニフェストでのアプリケーション Id の検索**

インストールされている UWP アプリのマニフェストファイルでアプリケーション Id を検索するには、*アプリケーション id*のエントリを探します。

たとえば、hello world アプリの場合、アプリケーション ID は*app*です。

```xml
<Application Id="App"
      Executable="$targetnametoken$.exe"
      EntryPoint="HelloWorld.App">
```

**WinDbg コマンドラインの例**

これは、完全なパッケージ名と AppId を使用して、デバッガーで HelloWorld アプリを読み込むコマンドラインの例です。

```console
windbg.exe -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

## <a name="span-idlaunching_a_background_task_under_the_debuggerspanspan-idlaunching_a_background_task_under_the_debuggerspanspan-idlaunching_a_background_task_under_the_debuggerspanlaunching-a-background-task-under-the-debugger"></a><span id="Launching_a_background_task_under_the_debugger"></span><span id="launching_a_background_task_under_the_debugger"></span><span id="LAUNCHING_A_BACKGROUND_TASK_UNDER_THE_DEBUGGER"></span>デバッガーでのバックグラウンドタスクの起動


バックグラウンドタスクは、コマンドラインから TaskId を使用して、デバッガーで明示的に起動できます。 これを行うには、-plmPackage パラメーターと-plmBgTaskId コマンドラインパラメーターを使用します。

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
<td align="left"><p>アプリケーションパッケージの名前。 Querypackages コマンドを使用して、すべての UWP アプリケーションを一覧表示します。 パッケージの場所へのパスを指定せずに、パッケージ名だけを指定してください。</p></td>
</tr>
<tr class="odd">
<td align="left">&lt;BackgroundTaskId&gt;</td>
<td align="left"><p>BackgroundTaskId は、以下で説明するように、querypackages コマンドを使用して見つけることができます。</p>
<p>アプリケーションマニフェストファイルの詳細については、「アプリケーション<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">パッケージマニフェスト</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

デバッガーで SDKSamples タスクコードを読み込む例を次に示します。

```console
windbg.exe -plmPackage Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe -plmBgTaskId {ee4438ee-22db-4cdd-85e4-8ad8a1063523}
```

バックグラウンドタスクのサンプルコードを試して、UWP デバッグに慣れることができます。 [バックグラウンドタスクのサンプル](https://go.microsoft.com/fwlink/p/?linkid=2112776)でダウンロードできます。

Querypackages コマンドを使用して、BackgroundTaskId を検索します。 CTRL + F キーを使用してアプリを検索し、[*バックグラウンドタスク Id* ] フィールドを探します。 バックグラウンドタスクは、関連付けられているバックグラウンドタスク名とタスク Id を表示するために実行されている必要があります。

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

完全なパッケージ名がわかっている場合は、. querypackage を使用して [*バックグラウンドタスク Id* ] フィールドを表示できます。

PLMDebug の enumerateBgTasks オプションを使用して、BackgroundTaskId を検索することもできます。 PMLDebug utiltity の詳細については、「 [**Plmdebug**](plmdebug.md)」を参照してください。

```console
C:\Program Files\Debugging Tools for Windows (x64)>PLMDebug /enumerateBgTasks Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe
Package full name is Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe.
Background Tasks:
SampleBackgroundTask : {C05806B1-9647-4765-9A0F-97182CEA5AAD}

SUCCEEDED
```

## <a name="span-iddebugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_spanspan-iddebugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_spanspan-iddebugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_spandebugging-a-uwp-process-remotely-using-a-process-server-dbgsrv"></a><span id="Debugging_a_UWP_process_remotely_using_a_Process_Server__DbgSrv_"></span><span id="debugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_"></span><span id="DEBUGGING_A_UWP_PROCESS_REMOTELY_USING_A_PROCESS_SERVER__DBGSRV_"></span>プロセスサーバー (DbgSrv) を使用したリモートでの UWP プロセスのデバッグ


-Plm srv では、すべての-plm\* コマンドが正常に動作します。 Dbgsrv を使用してデバッグするには、-premote スイッチと dbgsrv の接続文字列を使用します。

```console
windbg.exe -premote npipe:pipe=fdsa,server=localhost -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

-Premote オプションの詳細については、「[プロセスサーバー (ユーザーモード)](process-servers--user-mode-.md) 」および「[プロセスサーバーの例](process-server-examples.md)」を参照してください。

## <a name="span-idsummary_of_uwp_app_commandsspanspan-idsummary_of_uwp_app_commandsspanspan-idsummary_of_uwp_app_commandsspansummary-of-uwp-app-commands"></a><span id="Summary_of_UWP_app_commands"></span><span id="summary_of_uwp_app_commands"></span><span id="SUMMARY_OF_UWP_APP_COMMANDS"></span>UWP アプリのコマンドの概要


このセクションでは、UWP アプリデバッガーコマンドの概要について説明します。

**パッケージ情報を収集しています**

**.querypackage**

Querypackage は、UWP アプリケーションの状態を表示します。 たとえば、アプリが実行されている場合は、*アクティブな*状態になることがあります。

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

Querypackages コマンドは、インストールされているすべての UWP アプリケーションとその現在の状態を一覧表示します。

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

**デバッグ用のアプリの起動**

**. createpackageapp**

Createpackageapp コマンドは、デバッグを有効にし、UWP アプリケーションを起動します。

```dbgcmd
.createpackageapp <PLMPackageName> <ApplicationId> [<parameters>] 
```

次の表に、createpackageapp のパラメーターの一覧を示します。

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
<td align="left">アプリケーションパッケージの名前。 Querypackages コマンドを使用して、すべての UWP アプリケーションを一覧表示します。 パッケージの場所へのパスを指定せずに、パッケージ名だけを指定してください。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>ApplicationId は、このトピックで既に説明したように、. querypackage または querypackages を使用して見つけることができます。</p>
<p>アプリケーションマニフェストファイルの詳細については、「アプリケーション<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">パッケージマニフェスト</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;パラメーター&gt;]</td>
<td align="left">アプリケーションに渡される省略可能なパラメーター。 これらの省略可能なパラメーターを必要としないアプリケーションもあります。</td>
</tr>
</tbody>
</table>

 

以下に例を示します。

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

**デバッグコマンドの使用を有効または無効にする**

**. enablepackagedebug**

. Enablepackagedebug コマンドは、UWP アプリケーションのデバッグを有効にします。 Suspend、resume、または terminate 関数のいずれかを呼び出す前に、. enablepackagedebug を使用する必要があります。

Createpackageapp コマンドでは、アプリのデバッグも有効になっていることに注意してください。

```dbgcmd
.enablepackagedebug <PLMPackageName>
```

以下に例を示します。

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**. disablepackagedebug**

. Disablepackagedebug コマンドは、UWP アプリケーションのデバッグを無効にします。

```dbgcmd
.disablepackagedebug <PLMPackageName>
```

以下に例を示します。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**アプリの開始と停止**

中断、再開、および終了は、パッケージ内で現在実行中のすべてのアプリに影響します。

**.suspendpackage**

Suspendpackage コマンドは、UWP アプリケーションを中断します。

```dbgcmd
.suspendpackage <PLMPackageName> 
```

以下に例を示します。

```dbgcmd
0:024> .suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.resumepackage**

Resumepackage コマンドは、UWP アプリケーションを再開します。

```dbgcmd
.resumepackage <PLMPackageName> 
```

以下に例を示します。

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.terminatepackageapp**

Terminatepackageapp コマンドは、パッケージ内のすべての UWP アプリケーションを終了します。

```dbgcmd
.terminatepackageapp <PLMPackageName> 
```

以下に例を示します。

```dbgcmd
.terminatepackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**バックグラウンド タスク**

**.activatepackagebgtask**

Activatepackagebgtask コマンドは、デバッグを有効にし、UWP バックグラウンドタスクを起動します。

```dbgcmd
 .activatepackagebgtask <PLMPackageName> <bgTaskId>
```

以下に例を示します。

```dbgcmd
.activatepackagebgtask Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe {C05806B1-9647-4765-9A0F-97182CEA5AAD}
```

## <a name="span-idusage_examplesspanspan-idusage_examplesspanspan-idusage_examplesspanusage-examples"></a><span id="Usage_Examples"></span><span id="usage_examples"></span><span id="USAGE_EXAMPLES"></span>使用例


**アプリが起動されたときにデバッガーをアタッチする**

HelloWorld という名前のアプリがあり、e24caf14-8483-4743-b80c-ca46c28c75df\_1.0.0.0\_x86\_\_97ghe447vaan8 という名前のパッケージに含まれているとします。 完全な名前を表示し、インストールされているすべてのパッケージを実行して、パッケージがインストールされていることを確認します。 コマンドプロンプトウィンドウで、次のコマンドを入力します。 CTRL + F を使用して、コマンドの出力で HelloWorld のアプリ名を検索できます。

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

Createpackageapp を使用してアプリを起動し、アプリにアタッチします。 また、createpackageapp コマンドを使用すると、アプリのデバッグも有効になります。

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

デバッグが完了したら、. disablepackagedebug コマンドを使用して、パッケージのデバッグ参照カウントをデクリメントします。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**既に実行中のアプリにデバッガーをアタッチする**

既に実行されているである、MyApp に WinDbg をアタッチするとします。 WinDbg の **ファイル** メニューで、**プロセスにアタッチ** を選択します。 MyApp のプロセス ID をメモしておきます。 たとえば、プロセス ID が4816であるとします。 MyApp を含むパッケージのデバッグ参照カウントをインクリメントします。

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

WinDbg の **プロセスにアタッチ** ダイアログボックスで、プロセス 4816 を選択し、OK をクリックします。 WinDbg が MyApp にアタッチされます。

デバッグが完了したら、. disablepackagedebug コマンドを使用して、パッケージのデバッグ参照カウントをデクリメントします。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**アプリを手動で中断して再開する**

アプリを手動で中断して再開するには、次の手順に従います。 最初に、アプリを含むパッケージのデバッグ参照カウントをインクリメントします。

```dbgcmd
.enablepackagedebug  e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

パッケージを中断します。 アプリの中断ハンドラーが呼び出されます。これはデバッグに役立ちます。

```dbgcmd
.suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

デバッグが完了したら、パッケージを再開します。

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

最後に、パッケージのデバッグ参照カウントをデクリメントします。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WinDbg を使用したデバッグ](debugging-using-windbg.md)

 

 







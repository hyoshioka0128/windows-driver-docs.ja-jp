---
title: WinDbg を使用したユーザーモード プロセスのデバッグ
description: 実行中のプロセスにアタッチするまたは生成し、新しいプロセスにアタッチするのには、WinDbg を使用できます。
ms.assetid: 65677DE4-4C91-4E24-B9BC-0924619C7307
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a01ee2d466725d3ec9000de00af43ab85bec12ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359065"
---
# <a name="span-iddebuggerdebuggingauser-modeprocessusingwindbgspandebugging-a-user-mode-process-using-windbg"></a><span id="debugger.debugging_a_user-mode_process_using_windbg"></span>WinDbg を使用してユーザー モード プロセスのデバッグ


実行中のプロセスにアタッチするまたは生成し、新しいプロセスにアタッチするのには、WinDbg を使用できます。

## <a name="span-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanspan-idattachingtoarunningprocessspanattaching-to-a-running-process"></a><span id="Attaching_to_a_Running_Process"></span><span id="attaching_to_a_running_process"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS"></span>実行中のプロセスへのアタッチ


WinDbg を使用して、実行中のプロセスにアタッチするいくつかの方法はあります。 選択したメソッドに関係なく、プロセス ID またはプロセス名を必要があります。 プロセス ID は、オペレーティング システムによって割り当てられた番号です。 プロセス ID と、プロセス名を確認する方法の詳細については、次を参照してください。[プロセス ID の検索](finding-the-process-id.md)します。

### <a name="span-idwindbgmenuspanspan-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="WinDbg_Menu"></span><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg のメニュー

選択して、実行中のプロセスにアタッチできます WinDbg が休止モードのときは、**プロセスにアタッチする**から、**ファイル**メニューまたはキーを押して**F6**します。

**プロセスにアタッチ** ダイアログ ボックスで、デバッグ、およびをクリックするプロセスを選択**OK**します。

### <a name="span-idcommandprompt1spanspan-idcommandprompt1spancommand-prompt"></a><span id="command_prompt1"></span><span id="COMMAND_PROMPT1"></span>コマンド プロンプト

コマンド プロンプト ウィンドウを実行中のプロセスにアタッチできます WinDbg を起動するときに。 次のコマンドのいずれかを使用します。

-   **windbg -p** *ProcessID*
-   **windbg -pn** *ProcessName*

場所*ProcessID*が実行中のプロセスのプロセス ID または*ProcessName*実行中のプロセスの名前を指定します。

コマンドライン構文の詳細については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。

### <a name="span-iddebuggercommandwindow1spanspan-iddebuggercommandwindow1spandebugger-command-window"></a><span id="debugger_command_window1"></span><span id="DEBUGGER_COMMAND_WINDOW1"></span>デバッガー コマンド ウィンドウ

使用して実行中のプロセスにアタッチすることができる場合、WinDbg では、1 つまたは複数のプロセスをデバッグは既に、 [ **.attach (プロセスにアタッチ)** ](-attach--attach-to-process-.md)コマンド、[デバッガー コマンド ウィンドウ](the-debugger-command-window.md).

常に、デバッガーは同時に、複数のターゲット プロセスを開始し、いくつかのスレッドの固定または中断しない限り、します。

場合、 [ **.attach** ](-attach--attach-to-process-.md)コマンドが成功すると、デバッガーでは、次回デバッガー実行コマンドを発行するを指定されたプロセスにアタッチします。 行でこのコマンド何回かを使用する場合実行を何度でも、このコマンドを使用すると、デバッガーによって要求される必要があります。

## <a name="span-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanspan-idattachingtoarunningprocessnoninvasivelyspanattaching-to-a-running-process-noninvasively"></a><span id="Attaching_to_a_Running_Process_Noninvasively"></span><span id="attaching_to_a_running_process_noninvasively"></span><span id="ATTACHING_TO_A_RUNNING_PROCESS_NONINVASIVELY"></span>Noninvasively 実行中のプロセスにアタッチ


実行中のプロセスをデバッグし、わずかに干渉するかどうか、その実行には、プロセスをデバッグする必要があります[noninvasively](noninvasive-debugging--user-mode-.md)します。

### <a name="span-idwindbgmenu1spanspan-idwindbgmenu1spanwindbg-menu"></a><span id="windbg_menu1"></span><span id="WINDBG_MENU1"></span>WinDbg のメニュー

選択して、実行中のプロセスをデバッグできます noninvasively WinDbg が休止モード、**プロセスにアタッチする**から、**ファイル**メニューまたはキーを押して**F6**します。

ときに、**プロセスにアタッチ** ダイアログ ボックスが表示されたら、選択、 **Noninvasive**チェック ボックスをオンします。 次に、プロセス ID と名前を含む行を選択します。 (プロセス ID を入力することも、**プロセス ID**ボックス)。最後に、クリックして**OK**します。

### <a name="span-idcommandprompt2spanspan-idcommandprompt2spancommand-prompt"></a><span id="command_prompt2"></span><span id="COMMAND_PROMPT2"></span>コマンド プロンプト

コマンド プロンプト ウィンドウで割り当てることができます、実行中のプロセスに noninvasively WinDbg を起動するときにします。 次のコマンドのいずれかを使用します。

**windbg の pv-p** *ProcessID*
**windbg -pv-pn** *ProcessName*はいくつかその他の便利なコマンド ライン オプションがあります。 コマンドライン構文の詳細については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。

### <a name="span-iddebuggercommandwindow2spanspan-iddebuggercommandwindow2spandebugger-command-window"></a><span id="debugger_command_window2"></span><span id="DEBUGGER_COMMAND_WINDOW2"></span>デバッガー コマンド ウィンドウ

Noninvasively を使用して実行中のプロセスをデバッグすることができます、デバッガーが既にアクティブである場合、 [ **.attach v (プロセスにアタッチ)** ](-attach--attach-to-process-.md)コマンド、[デバッガー コマンド ウィンドウ](the-debugger-command-window.md)します。

使用することができます、 **.attach**かどうか、デバッガーは、1 つまたは複数のプロセスの invasively デバッグ既にコマンドします。 WinDbg を休止状態にした場合は、このコマンドを使用することはできません。

場合、 **.attach v**コマンドが成功すると、デバッガーは、次回のデバッガー実行コマンドを発行する、指定されたプロセスをデバッグします。 待合室デバッグ中に実行が許可されていないため、デバッガーが、一度に 1 つ以上のプロセスをデバッグできません noninvasively。 この制限を使用することを意味も、 **.attach v**コマンドことは、既存の干渉のデバッグ セッションあまり役に立ちません。

## <a name="span-idspawninganewprocessspanspan-idspawninganewprocessspanspan-idspawninganewprocessspanspawning-a-new-process"></a><span id="Spawning_a_New_Process"></span><span id="spawning_a_new_process"></span><span id="SPAWNING_A_NEW_PROCESS"></span>新しいプロセスを作成


WinDbg では、ユーザー モード アプリケーションを起動でき、その後、アプリケーションをデバッグすることができます。 アプリケーションは、名前によって指定されます。 (元のターゲット プロセスを開始した追加のプロセス) の子プロセスにデバッガーも自動的にアタッチすることができます。

デバッガーが (子プロセスとも呼ばれます) を作成するプロセスにデバッガーが作成していないプロセスよりも若干異なる方法で動作します。

標準ヒープ API を使用する代わりには、デバッガーが作成するプロセスは、特別なデバッグ ヒープを使用します。 使用して、デバッグ ヒープではなく標準ヒープを使用する子プロセスを強制することができます、\_いいえ\_デバッグ\_ヒープ[環境変数](general-environment-variables.md)または **-hd**コマンド ライン オプション。

また、対象アプリケーションは、デバッガーの子プロセスであるために、デバッガーのアクセス許可を継承します。 このアクセス許可には、それ以外の場合を実行できなかった特定のアクションを実行する対象のアプリケーションが有効にすることがあります。 たとえば、対象アプリケーションは保護されているプロセスを制御することにあります。

### <a name="span-idwindbmenu2spanspan-idwindbmenu2spanwindbg-menu"></a><span id="windb_menu2"></span><span id="WINDB_MENU2"></span>WinDbg のメニュー

WinDbg が休止モードのときを選択して、新しいプロセスを起動したことができます**実行可能ファイルのオープン**から、**ファイル**メニューまたは CTRL + E キーを押します。

開いている実行可能 ダイアログ ボックスが表示されたらで実行可能ファイルの完全なパスを入力してください。、**ファイル名**ボックス、またはを使用して、**ファイルの場所**一覧するパスとファイル名を選択します。

ユーザー モード アプリケーションでコマンド ライン パラメーターを使用する場合は、それらを入力します。、**引数**ボックス。 既定のディレクトリから開始ディレクトリを変更する場合は、ディレクトリのパスを入力してください。、**開始**ディレクトリ ボックス。 WinDbg を子プロセスにアタッチする場合は、選択、**も子プロセスのデバッグ**チェック ボックスをオンします。

選択した後に、クリックして**オープン**します。

### <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>コマンド プロンプト

WinDbg を起動するときに、コマンド プロンプト ウィンドウで、新しいプロセスを生成できます。 次のコマンドを使用します。

**windbg \[-o\]**  *ProgramName* **\[**<em>引数</em>**\]**

**-O**オプションにより、デバッガーの子プロセスにアタッチします。 いくつかその他の便利なコマンド ライン オプションがあります。 コマンドライン構文の詳細については、次を参照してください。 [ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。

### <a name="span-iddebuggercommandwindow3spanspan-iddebuggercommandwindow3spandebugger-command-window"></a><span id="debugger_command_window3"></span><span id="DEBUGGER_COMMAND_WINDOW3"></span>デバッガー コマンド ウィンドウ

使用して、新しいプロセスを作成するには WinDbg は 1 つまたは複数のプロセスをデバッグして既に場合、 [ **(プロセスの作成) に関する**](-create--create-process-.md)コマンド、[デバッガー コマンド ウィンドウ](the-debugger-command-window.md)します。

デバッガーは常に対象プロセスを複数同時に開始、いくつかのスレッドの凍結または中断がない限り。

場合、 [**に関する**](-create--create-process-.md)コマンドが成功すると、デバッガーは、次回のデバッガー実行コマンドを発行する、指定されたプロセスを作成します。 行でこのコマンド何回かを使用する場合実行を何度でも、このコマンドを使用すると、デバッガーによって要求される必要があります。

使用して、アプリケーションの開始ディレクトリを制御することができます、 [ **.createdir (作成プロセス ディレクトリの設定)** ](-createdir--set-created-process-directory-.md)する前にコマンド[**に関する**](-create--create-process-.md). 使用することができます、 **.createdir-は**コマンドまたは **- noinh**ターゲット アプリケーションが、デバッガーのハンドルを継承するかどうかを制御するコマンド ライン オプション。

アクティブ化またはを使用して子プロセスのデバッグを非アクティブ化することができます、 [ **.childdbg (子プロセスのデバッグ)** ](-childdbg--debug-child-processes-.md)コマンド。

## <a name="span-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanspan-idreattachingtoaprocessspanreattaching-to-a-process"></a><span id="Reattaching_to_a_Process"></span><span id="reattaching_to_a_process"></span><span id="REATTACHING_TO_A_PROCESS"></span>プロセスに再アタッチ


デバッガーでは、応答を停止したり、フリーズする場合、は、ターゲット プロセスに新しいデバッガーを添付できます。 このような状況でデバッガーをアタッチする方法の詳細については、次を参照してください。[対象アプリケーションを再アタッチ](reattaching-to-the-target-application.md)します。

 

 






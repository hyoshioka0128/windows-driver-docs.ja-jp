---
title: 待合室デバッグ (ユーザー モード)
description: 待合室デバッグ (ユーザー モード)
ms.assetid: 91f09fb1-9f5e-4081-89b3-78c95eada817
keywords:
- noninvasively デバッグ プロセス
- 待合室デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7474dabd0cbf06f71ab7ca976aa848e4eef21a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559470"
---
# <a name="noninvasive-debugging-user-mode"></a>待合室デバッグ (ユーザー モード)


## <span id="ddk_noninvasive_debugging_user_mode__dbg"></span><span id="DDK_NONINVASIVE_DEBUGGING_USER_MODE__DBG"></span>


デバッガーとデバッグ、ユーザー モード アプリケーションが既に実行されている場合*noninvasively*します。 待合室のデバッグが、多くのデバッグ操作がありません。 ただし、対象のアプリケーションで、デバッガーの干渉を最小限に抑えることができます。 待合室デバッグは、ターゲット アプリケーションが応答しなくなった場合に便利です。

待合室デバッグで、デバッガーは実際にアタッチできません、ターゲット アプリケーションにします。 デバッガーでは、すべてのターゲットのスレッドを中断し、ターゲットのメモリ、レジスタ、およびその他のような情報にアクセスします。 ただし、デバッガー制御できない、ターゲット コマンドよう[ **g (移動)** ](g--go-.md)機能しません。

状態、「デバッガーがアタッチされていません、ため、プロセスの実行を監視することはできません」エラー メッセージが表示される待合室デバッグ中に許可されていないコマンドを実行しようとすると、

### <a name="span-idselectingtheprocesstodebugspanspan-idselectingtheprocesstodebugspanselecting-the-process-to-debug"></a><span id="selecting_the_process_to_debug"></span><span id="SELECTING_THE_PROCESS_TO_DEBUG"></span>デバッグするプロセスを選択します。

プロセス ID (PID) でターゲット アプリケーションまたはプロセス名を指定することができます。

名前で、アプリケーションを指定する場合は、ファイル名拡張子を含む、プロセスの完全な名前を使用する必要があります。 2 つのプロセスの同じ名前である場合は、代わりにプロセス ID を使用する必要があります。

プロセス ID と、プロセス名を確認する方法の詳細については、[プロセス ID の検索](finding-the-process-id.md)を参照してください。

開始と待合室デバッグ セッションを停止する方法については、次のトピックを参照してください。

-   [Visual Studio を使用してユーザー モード プロセスのデバッグ](debugging-a-user-mode-process-using-visual-studio.md)
-   [WinDbg を使用してユーザー モード プロセスのデバッグ](debugging-a-user-mode-process-using-windbg.md)
-   [CDB を使用してユーザー モード プロセスのデバッグ](debugging-a-user-mode-process-using-cdb.md)

### <a name="span-idcdbcommandlinespanspan-idcdbcommandlinespancdb-command-line"></a><span id="cdb_command_line"></span><span id="CDB_COMMAND_LINE"></span>CDB コマンドライン

Noninvasively CDB コマンドラインから実行中のプロセスをデバッグするには、次の構文 -pv オプション、-p オプション、およびプロセス ID を指定します。

**cdb -pv -p** *ProcessID*

または、noninvasively プロセス名を指定して実行中のプロセスをデバッグするには次の構文を代わりに使用します。

**cdb -pv -pn** *ProcessName*

いくつかその他の便利なコマンド ライン オプションがあります。 コマンドライン構文の詳細については、[ **CDB コマンド ライン オプション**](cdb-command-line-options.md)を参照してください。

### <a name="span-idwindbgcommandlinespanspan-idwindbgcommandlinespanwindbg-command-line"></a><span id="windbg_command_line"></span><span id="WINDBG_COMMAND_LINE"></span>WinDbg コマンド ライン

Noninvasively WinDbg のコマンドラインから実行中のプロセスをデバッグするには、次の構文 -pv オプション、-p オプション、およびプロセス ID を指定します。

**windbg -pv -p** *ProcessID*

または、noninvasively プロセス名を指定して実行中のプロセスをデバッグするには次の構文を代わりに使用します。

**windbg -pv -pn** *ProcessName*

いくつかその他の便利なコマンド ライン オプションがあります。 コマンドライン構文の詳細については、[ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)を参照してください。

### <a name="span-idwindbgmenuspanspan-idwindbgmenuspanwindbg-menu"></a><span id="windbg_menu"></span><span id="WINDBG_MENU"></span>WinDbg のメニュー

WinDbg が休止モード、または F6 キーを押して ファイル メニューのプロセスにアタッチ をクリックして、実行中のプロセス noninvasively デバッグできます。

[アタッチするプロセス] ダイアログ ボックスが表示されたら、待合室のチェック ボックスを選択します。 次に、プロセス ID と名前を含む行を選択します。 (入力することも、プロセス ID、プロセス ID ボックスにします。)最後に、ok をクリックします。

### <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウ

Noninvasively を使用して実行中のプロセスをデバッグすることができます、デバッガーが既にアクティブである場合、 [ **.attach v (プロセスにアタッチ)** ](-attach--attach-to-process-.md)コマンド、[デバッガー コマンド ウィンドウ](the-debugger-command-window.md)します。

場合は、デバッガーは、1 つまたは複数のプロセスの invasively デバッグ既に .attach コマンドを使用できます。 休止 WinDbg ではなく CDB が休止状態にある場合に、このコマンドを使用することができます。

.Attach-v コマンドが成功した場合、デバッガーは、次回のデバッガー実行コマンドを発行する、指定されたプロセスをデバッグします。 待合室デバッグ中に実行が許可されていないため、デバッガーが、一度に 1 つ以上のプロセスをデバッグできません noninvasively。 この制限は、.attach - v のコマンドを使用して可能性がありますように既存の干渉のデバッグ セッションほど便利でも意味します。

### <a name="span-idbeginningthedebuggingsessionspanspan-idbeginningthedebuggingsessionspanbeginning-the-debugging-session"></a><span id="beginning_the_debugging_session"></span><span id="BEGINNING_THE_DEBUGGING_SESSION"></span>デバッグ セッションを開始

デバッグ セッションを開始する方法の詳細については、[デバッガー操作](debugger-operation-win8.md)を参照してください。

 

 






---
title: Remote.exe セッションの開始
description: Remote.exe セッションの開始
ms.assetid: 2b70e54e-ab02-46f1-9af1-e7379c89cf3c
keywords:
- セッションの開始、remote.exe を通じてリモート デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2dfd1da6a4f1aa9c24a97dacc3d0c3ac0089dc0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335537"
---
# <a name="starting-a-remoteexe-session"></a>Remote.exe セッションの開始


## <span id="ddk_starting_a_remote_exe_session_dbg"></span><span id="DDK_STARTING_A_REMOTE_EXE_SESSION_DBG"></span>


KD、CDB と remote.exe セッションを開始する 2 つの方法はあります。 これらのメソッドの 2 番目のだけは NTSD で動作します。

### <a name="span-idcustomizingyourcommandpromptwindowspanspan-idcustomizingyourcommandpromptwindowspancustomizing-your-command-prompt-window"></a><span id="customizing_your_command_prompt_window"></span><span id="CUSTOMIZING_YOUR_COMMAND_PROMPT_WINDOW"></span>コマンド プロンプト ウィンドウをカスタマイズします。

Remote.exe クライアントと Remote.exe サーバーは、コマンド プロンプト ウィンドウで実行します。

をリモート セッションで準備するには、使いやすさを向上させるには、このウィンドウをカスタマイズする必要があります。 コマンド プロンプト ウィンドウを開きます。 タイトル バーを右クリックして**プロパティ**します。 選択、**レイアウト**タブ。「画面バッファーのサイズ」と入力のタイトル セクションに移動し**90**で、**幅**ボックスとの間の値**4000**と**9999** で**高さ**ボックス。 カーネル デバッガーをリモート セッションでのスクロール バーを有効にします。

コマンド プロンプトの形状を変更する場合は、「Windows サイズ」セクションの幅と高さ値を変更します。 選択、**オプション**タブ。有効にする、**編集オプション**簡易編集モードと挿入モード。 これにより、コマンド プロンプト セッションで情報をコピー アンド ペーストをことができます。 **[OK]** をクリックして変更を適用します。 今後のすべてのセッションに変更を適用するオプションを選択を求められたらします。

### <a name="span-idstartingtheremoteexeserverfirstmethodspanspan-idstartingtheremoteexeserverfirstmethodspanstarting-the-remoteexe-server-first-method"></a><span id="starting_the_remote_exe_server__first_method"></span><span id="STARTING_THE_REMOTE_EXE_SERVER__FIRST_METHOD"></span>Remote.exe サーバーを開始するには。最初のメソッド

Remote.exe サーバーを起動するための一般的な構文は次のとおりです。

```console
remote /s "Command_Line" Unique_Id [/f Foreground_Color] [/b Background_Color] 
```

これは、次の例のように、リモート コンピューターの KD、CDB またはの開始を使用できます。

```console
remote /s "KD [options]" MyBrokenBox 

remote /s "CDB [options]" MyBrokenApp 
```

これは、コマンド プロンプト ウィンドウで Remote.exe サーバーを起動し、デバッガーを起動します。

呼び出されたよりも、別のウィンドウで、NTSD プロセスが実行されるため、直接、NTSD を起動するのにこのメソッドを使用できません。

### <a name="span-idstartingtheremoteexeserversecondmethodspanspan-idstartingtheremoteexeserversecondmethodspanstarting-the-remoteexe-server-second-method"></a><span id="starting_the_remote_exe_server__second_method"></span><span id="STARTING_THE_REMOTE_EXE_SERVER__SECOND_METHOD"></span>Remote.exe サーバーを開始するには。2 番目のメソッド

Remote.exe サーバーを起動できる別の方法があります。 このメソッドは、まず、デバッガーを起動しを使用して、 [ **.remote (Remote.exe サーバーの作成)** ](-remote--create-remote-exe-server-.md)サーバーを起動するコマンド。

以降、 **.remote**コマンドが発行されるは、デバッガーが開始した後、このメソッドは同等に機能 KD、CDB、NTSD に連動します。

次に例を示します。 最初に、通常の方法で、デバッガーを起動します。

```console
KD [options] 
```

デバッガーが実行されている場合、使用、 **.remote**コマンド。

```dbgcmd
.remote MyBrokenBox 
```

これは、結果、最初のメソッドと同様に正確にも"MyBrokenBox"の ID を持つ Remote.exe サーバーである KD プロセス。

このメソッドの利点の 1 つは、リモート デバッグを使用する場合、事前に決定する必要はありません。 コンソール デバッガーのいずれかをデバッグしようし、し、決定をだれかが、リモートの場所を引き継ぐ場合は、使用することができる場合、 **.remote**コマンドと、セッションに接続できます。

### <a name="span-idstartingtheremoteexeclientspanspan-idstartingtheremoteexeclientspanstarting-the-remoteexe-client"></a><span id="starting_the_remote_exe_client"></span><span id="STARTING_THE_REMOTE_EXE_CLIENT"></span>Remote.exe クライアントを開始

Remote.exe クライアントを起動するための一般的な構文は次のとおりです。

```console
remote /c ServerNetBIOSName Unique_ID [/l Lines_to_Get] [/f Foreground_Color] [/b Background_Color] 
```dbgcmd

For example, if the "MyBrokenBox" session, described above, was started on a local host computer whose network name was "Server2", you can connect to it with the command:

```console
remote /c server2 MyBrokenBox 
```

適切なアクセス許可を持つネットワーク上のすべてのユーザー、コンピューター名とセッション ID がわかっている限り、このデバッグ セッションを接続することができます。

### <a name="span-idissuingcommandsspanspan-idissuingcommandsspanissuing-commands"></a><span id="issuing_commands"></span><span id="ISSUING_COMMANDS"></span>コマンドの発行

コマンドは、Remote.exe クライアントを通じて発行され、Remote.exe サーバーに送信されます。 デバッガーに直接入力された場合、クライアントに任意のコマンドを入力できます。

Remote.exe クライアントで remote.exe セッションを終了するには、入力、 <strong>@Q</strong>コマンド。 これにより、Remote.exe サーバーと、デバッガーを実行できます。

サーバー セッションを終了するには、入力、 <strong>@K</strong> Remote.exe サーバーでコマンド。

 

 






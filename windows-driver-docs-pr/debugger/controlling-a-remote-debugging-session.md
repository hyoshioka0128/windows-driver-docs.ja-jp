---
title: リモート デバッグ セッションの制御
description: リモート デバッグ セッションの制御
ms.assetid: dedd277d-1aa0-468c-919c-29b25b0b5c0d
keywords:
- セッションを制御する、デバッガーからのリモート デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 165f4973c870d4071942521f4eb87e27672d7a94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375536"
---
# <a name="controlling-a-remote-debugging-session"></a>リモート デバッグ セッションの制御


## <span id="ddk_controlling_a_remote_debugging_session_dbg"></span><span id="DDK_CONTROLLING_A_REMOTE_DEBUGGING_SESSION_DBG"></span>


リモート セッションが開始されると、デバッグのサーバーまたはデバッグのクライアントのいずれかにコマンドを入力できます。 複数のクライアントがある場合は、コマンドを入力することができます。 ENTER を押すと、コマンドがデバッグ サーバーに送信し、実行します。

1 人のユーザーがコマンドを入力するたびに、すべてのユーザーは、コマンド自体とその出力に表示されます。 デバッグ クライアントからこのコマンドを発行した場合、その他のすべてのユーザーは上記のコマンドを発行するユーザーのコマンド、id で表示されます。 デバッグ サーバーから発行されたコマンドには、このプレフィックスはありません。

1 人のユーザーは、コマンドを実行した後、KD、CDB または経由で接続されている他のユーザーには、新しいコマンド プロンプトは表示されません。 その一方で、デバッガー エンジンが実行されている場合でも、WinDbg のユーザーはデバッガー コマンド ウィンドウの下部のパネルでプロンプトを表示する継続的に、されます。 どちらもする必要があります行動はアラームの原因を。すべてのユーザーはいつでも、コマンドを入力することができ、エンジンは、受信した順序でこれらのコマンドを実行します。

インターフェイスは、デバッグ サーバーで実行することも、WinDbg で実行されるアクション。

### <a name="span-idcommunicationbetweenusersspanspan-idcommunicationbetweenusersspancommunication-between-users"></a><span id="communication_between_users"></span><span id="COMMUNICATION_BETWEEN_USERS"></span>ユーザーの間の通信

新しいデバッグ クライアント セッションに接続すると、その他のすべてのユーザーにはこのクライアントが接続されているメッセージが表示されます。 クライアントが切断されると、メッセージは表示されません。

[ **.Clients (デバッグ クライアントを一覧表示)** ](-clients--list-debugging-clients-.md)コマンドには、現在のデバッグ セッションに接続されているすべてのクライアントが一覧表示します。

[ **.Echo (エコー コメント)** ](-echo--echo-comment-.md)コマンドは 1 人のユーザーからのメッセージを送信するのに便利です。

### <a name="span-idwindbgworkspacesspanspan-idwindbgworkspacesspanwindbg-workspaces"></a><span id="windbg_workspaces"></span><span id="WINDBG_WORKSPACES"></span>WinDbg ワークスペース

WinDbg は、デバッグのクライアントとして使用されている、ときに、そのワークスペースはグラフィカル インターフェイスから値が設定のみを保存します。 デバッガー コマンド ウィンドウで加えられた変更は保存されません。 (これにより、ローカルのクライアントによって行われた変更のみ反映されます、デバッガー コマンド ウィンドウがデバッグ サーバーにすべてのクライアントからの入力を受け取るためです。)

### <a name="span-idfilepathsspanspan-idfilepathsspanfile-paths"></a><span id="file_paths"></span><span id="FILE_PATHS"></span>ファイル パス

シンボル パス、実行可能イメージのパス、および拡張 DLL のパスはすべてデバッグ サーバーで Windows のツールをデバッグ インストール フォルダーの相対ファイル パスとして解釈します。

WinDbg はデバッグのクライアントとして使用する場合は、独自*ローカル ソース パス*もします。 ソースに関連するすべてのコマンドは、ローカル コンピューターのソース ファイルにアクセスされます。 そのため、任意のクライアントまたはソース コマンドを使用するサーバーで設定する必要の適切なパスです。

この複数のパスのシステムでは、実際には、他のクライアントまたはサーバーとソース ファイルを共有することがなくソースに関連するコマンドを使用するクライアントはデバッグができます。 これは、秘密や機密ソース ファイルへのアクセスを持つユーザーのいずれかがある場合に便利です。

### <a name="span-idcancelingthedebuggingserverspanspan-idcancelingthedebuggingserverspancanceling-the-debugging-server"></a><span id="canceling_the_debugging_server"></span><span id="CANCELING_THE_DEBUGGING_SERVER"></span>デバッグ サーバーのキャンセル

[ **.Endsrv (エンド デバッグ サーバー)** ](-endsrv--end-debugging-server-.md)デバッグ サーバーを終了するコマンドを使用できます。 デバッガーがデバッグの複数のサーバーを確立している場合もまま他のユーザーとそれらの一部にキャンセルできますを実行します。

サーバーを終了して、将来のクライアントにアタッチされなくなります。 サーバーから現在接続されているすべてのクライアント切り取らこれはいません。

### <a name="span-idexitingthedebuggerandterminatingthesessionspanspan-idexitingthedebuggerandterminatingthesessionspanexiting-the-debugger-and-terminating-the-session"></a><span id="exiting_the_debugger_and_terminating_the_session"></span><span id="EXITING_THE_DEBUGGER_AND_TERMINATING_THE_SESSION"></span>デバッガーを終了して、セッションを終了しています

デバッグの 1 つのクライアントからサーバーを終了せずに終了するには、その特定のクライアントからコマンドを発行する必要があります。 このクライアントが KD、CDB またはの場合は、使用、 [ **CTRL + B** ](ctrl-b--quit-local-debugger-.md)を終了するキー。 KD、CDB またはを実行するスクリプトを使用する場合を使用して、 [ **.remote\_exit (終了デバッグ クライアント)**](-remote-exit--exit-debugging-client-.md)します。 このクライアントが WinDbg の場合は、選択**終了**から、**ファイル**を終了するメニュー。

セッション全体の処理をデバッグ、サーバーを終了するには、使用、 [ **q (終了)** ](q--qq--quit-.md)コマンド。 サーバーまたはクライアントからこのコマンドを入力することができ、すべてのユーザーの全体のセッションは終了します。

 

 






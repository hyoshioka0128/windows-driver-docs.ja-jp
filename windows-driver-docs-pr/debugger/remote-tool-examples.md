---
title: Remote ツールの例
description: Remote ツールの例
ms.assetid: 624f1a78-04da-45c2-8f8d-a593d557be7d
keywords:
- リモート ツール、例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: becf699b2abf896261d58426343abccbf7d28a1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570331"
---
# <a name="remote-tool-examples"></a>Remote ツールの例


## <span id="ddk_remote_tool_examples_dtools"></span><span id="DDK_REMOTE_TOOL_EXAMPLES_DTOOLS"></span>


このセクションの例では、リモート ツールの使用法を示すし、サンプルの入力と出力を表示します。

### <a name="span-idbasicservercommandspanspan-idbasicservercommandspanbasic-server-command"></a><span id="basic_server_command"></span><span id="BASIC_SERVER_COMMAND"></span>基本的なサーバー コマンド

次のコマンドは、コンピューターでリモート セッションを開始します。

コマンドを使用して、 **/s**パラメーターをサーバー側のコマンドを示します。 コマンドを使用して**cmd**Windows コマンド シェル (Cmd.exe) を起動するには、セッションの名前と**test1**します。

```console
remote /s cmd test1
```

応答では、リモート ツールは、セッションを開始し、クライアントを使用して、セッションに接続するコマンドが表示されます。

```console
**************************************
***********     REMOTE    ************
***********     SERVER    ************
**************************************
To Connect: Remote /C SERVER06 "test1"

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

### <a name="span-idbasicclientcommandspanspan-idbasicclientcommandspanbasic-client-command"></a><span id="basic_client_command"></span><span id="BASIC_CLIENT_COMMAND"></span>クライアントの基本的なコマンド

次のコマンドは、Server01 コンピューター上のリモート セッションに接続します。 コマンドを使用して、 **/c**クライアント側のコマンドを示します。 サーバーのコンピューターの名前を指定します**Server01**、そのコンピューターで、セッションの名前と**test1**します。

```console
remote /c server01 test1
```

応答では、リモート ツールには、クライアント コンピューターがサーバー コンピューター上のセッションに接続されていることを報告するメッセージが表示されます。 メッセージは、サーバー コンピューターとローカル ユーザーの名前を表示します (**Server04 user1**)。

```console
**************************************
***********     REMOTE    ************
***********     CLIENT    ************
**************************************
Connected...

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.

C:\Program Files\Debugging Tools for Windows>
**Remote: Connected to SERVER04 user1 [Tue 9:39 AM]
```

クライアントがサーバーに接続、両方が表示されます、クライアントとサーバー コンピューターでコマンド プロンプトから型指定されたコマンドが表示されます.

たとえば、入力した**dir**クライアントとサーバーの両方のコンピューターでコマンド プロンプト ウィンドウで、クライアント コンピューターのコマンド プロンプトでディレクトリの表示が表示されます。

### <a name="span-idusingserveroptionsspanspan-idusingserveroptionsspanusing-server-options"></a><span id="using_server_options"></span><span id="USING_SERVER_OPTIONS"></span>サーバー オプションを使用します。

次のサーバー側のコマンドは、NTSD デバッガーでリモート セッションを開始します。

コマンドを使用して、 **/s**パラメーターをサーバー側のコマンドを示します。 次のパラメーターでは、 **"v ntsd-d-"** デバッガーのオプションと、デバッガーを起動するコンソール コマンドです。 コンソール コマンドには、スペースが含まれているため、引用符で囲まれています。 コマンドには、セッションの名前が含まれています**debugit**します。

コマンドを使用して、 **/u**パラメーターは、コンピューターと、特定のユーザー、セッションに接続する、Domain01 にある User03 の管理者のみを許可するようにします。 使用して、 **/f**と **/b**白地に黒のテキスト (前景) を指定するオプション。

最後に、コマンドを使用して、 **/v**パラメーター、セッションのユーザー クエリを非表示にします。 デバッガー セッションは、既定で表示されます。

```console
remote /s "ntsd -d -v" DebugIt /u Administrators /u Domain01\User03 
/f black /b white /-v
```

応答では、リモート ツールは DebugIt という名前のセッションを作成し、指定されたパラメーターで NTSD を開始します。 メッセージは、指定されたユーザーのみに接続するアクセス許可があることを示します。 コマンド ウィンドウを指定した色に変更します。

```console
**************************************
***********     REMOTE    ************
***********     SERVER    ************
**************************************

Protected Server!  Only the following users or groups can connect:
    Administrators
    Domain01\User03
To Connect: Remote /C SERVER06 "debugit"

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

### <a name="span-idusingclientoptionsspanspan-idusingclientoptionsspanusing-client-options"></a><span id="using_client_options"></span><span id="USING_CLIENT_OPTIONS"></span>クライアントのオプションを使用します。

次のコマンドは、前の例で開始された NTSD デバッガーでのリモート セッションに接続します。

コマンドを使用して、 **/c**クライアント側のコマンドを示します。 サーバーのコンピューターの名前を指定します**server06**、リモート セッションの名前と**debugit**します。

コマンドにも含まれています、 **/k**キーワードの色のファイルの場所を指定するパラメーター。

```console
remote /c server06 debugit /k c:\remote_client.txt
```

色ファイルには、次のテキストが含まれます。

```console
Registry
white, blue
Token
red, white
```

このテキストでは、白の背景に赤いテキストで、リモート ツール、青い背景に白いテキストに単語"registry"(いない大文字小文字を区別) での出力の行を表示して、「トークン」と出力の行を表示するように指示します。

応答としては、リモート ツールは、クライアント、サーバー セッションを接続しますし、次のメッセージを表示します。

```console
**************************************
***********     REMOTE    ************
***********     CLIENT    ************
**************************************
Connected...

Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.
```

クライアントは、サーバー コンピューター上の NTSD デバッガーにコマンドを送信できるようになりました。 クライアントとサーバーの両方のコンピューターに、コマンドの出力が表示されます。

青色の背景と白い背景に赤いテキストでは、"kernel"という単語で出力の行に白いテキスト内のクライアント コンピューターには、"registry"と出力の行が表示されます。

### <a name="span-idqueryingasessionspanspan-idqueryingasessionspanquerying-a-session"></a><span id="querying_a_session"></span><span id="QUERYING_A_SESSION"></span>セッションのクエリを実行します。

リモート ツールには、クエリ パラメーターが含まれています (**/q**) 特定のコンピューターでリモート セッションの一覧を表示します。 表示されているセッションのみが含まれる (デバッガー セッションを開始せず、 **/v**パラメーターと、デバッガーなしのセッションの使用、 **/v**パラメーター)。

サーバーまたはクライアント コンピューターからのセッションを照会することができます。 ローカル コンピューター上のセッションのクエリを実行する場合でも、コンピューター名を指定する必要があります。

次のコマンドをローカル コンピューター上のセッションのクエリ**Server04**します。

```console
remote /q Server04
```

応答では、リモート ツールは、ローカル コンピューターで実行されているリモート セッションがないことを報告します。

```console
Querying server \\Server04
No Remote servers running on \\Server04
```

別のコンピューター上のセッションに関するクエリに応答して、これに対し、 **Server06**、リモート ツールには、そのコンピューターで実行されているセッションが表示されます。

```console
Querying server \\Server06

Visible sessions on server Server06:

ntsd                            [Remote /C SERVER06 "debug"] visible
cmd                             [Remote /C SERVER06 "test"] visible
```

表示のセッションでは、それらのセッション (NTSD およびコマンド プロンプト ウィンドウ) と、セッションに接続するコマンドで実行されているコンソール プログラムの一覧が表示されます。 引用符で囲まれたコマンドの構文には、セッション名が表示されます。

表示では、存在する場合、これらのセッションに対して確立されているアクセス許可は表示されません。 そのため、表示には追加するアクセス許可を持たないセッションが含まれます。

### <a name="span-idusingthesessioncommandsspanspan-idusingthesessioncommandsspanusing-the-session-commands"></a><span id="using_the_session_commands"></span><span id="USING_THE_SESSION_COMMANDS"></span>セッションのコマンドを使用します。

リモート セッション中にいつでも、リモート セッションのコマンドを使用することができます。

次のコマンドは、セッションに接続されているすべてのコンピューターにメッセージを送信します。

```console
@M I think I found the problem.
```

その結果、すべてのコンピューターのコマンド プロンプト ウィンドウでは、セッションで、メッセージが表示されます。 メッセージには、コンピューター名と、1 日とメッセージの日時が含まれています。

```console
@m I think I found the problem.     [SERVER01       Wed 11:53 AM]
```

サーバーのコンピューターから、メッセージが送信されると、コンピューター名の代わりに、ラベルには"Local"のことが表示されます。

```console
@m I think I found the problem.     [Local       Wed 11:52 AM]
```

次のコマンドでは、サーバー コンピューターに表示されるポップアップ メッセージが生成されます。 セッションのすべてのクライアント コンピューターでは、コマンド プロンプト ウィンドウにメッセージを書き込みます。

```console
@P Did you see that?
```

クライアント コンピューターで、ポップアップ メッセージは、コマンド ウィンドウに表示されます。

```console
From SERVER02  [Wed 11:58 AM]

 Did you see that?
```

メッセージ ラベルに表示される時刻は、メッセージを送信したクライアント コンピューターが別のタイム ゾーンである場合でも、サーバー コンピューターでは、時間では常にします。

### <a name="span-idendingaremotesessionspanspan-idendingaremotesessionspanending-a-remote-session"></a><span id="ending_a_remote_session"></span><span id="ENDING_A_REMOTE_SESSION"></span>リモート セッションを終了します。

次の例では、リモート セッションのコマンドを使用して、クライアント コンピューターをセッションから切断して、リモート セッションを終了する方法を示します。 リモート セッションを開始したサーバー コンピューターのみを終了できます。

クライアント コンピューターをクライアント コンピューターのリモート セッションから切断するには次のように入力します。  <strong>@q</strong>します。

応答では、切断されているクライアント コンピューターで、次のメッセージが表示されます。

```console
*** SESSION OVER ***
```

その他のすべてのコンピューターのセッションでは、リモート ツールは、切断された場合、ユーザー、コンピューターの名前を持つメッセージと日と切断の時間を投稿します。

```console
**Remote:  Disconnected from SERVER04 User01  [Wed 12:01 PM]
```

サーバー コンピューターのリモート セッションを終了するには、入力 <strong>@k</strong>します。 このコマンドは、クライアントを自動的に切断し、セッションを終了します。

 

 






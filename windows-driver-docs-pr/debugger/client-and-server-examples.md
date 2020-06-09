---
title: クライアントとサーバーの例
description: クライアントとサーバーの例
ms.assetid: 78dea1c0-6e94-4980-8042-375f11386d53
keywords:
- デバッガーを使用したリモートデバッグ、例
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6246d982f58faf8c55da9f10c9562a474ff3225d
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563168"
---
# <a name="client-and-server-examples"></a>クライアントとサーバーの例


## <span id="ddk_client_and_server_examples_dbg"></span><span id="DDK_CLIENT_AND_SERVER_EXAMPLES_DBG"></span>


たとえば、あるユーザーが* \\ \\ BOX17*という名前のコンピューターでアプリケーションを実行しているとします。 このアプリケーションには問題がありますが、デバッグ技術者は別のサイトにあります。

最初のユーザーは、 * \\ \\ BOX17*で CDB を使用してデバッグサーバーを設定します。 ターゲットアプリケーションのプロセス ID は122です。 TCP プロトコルが選択されており、ソケットポート番号は1025です。 サーバーを起動するには、管理者特権のコマンドプロンプトウィンドウで次のコマンドを入力します ([管理者として実行])。

```console
E:\Debugging Tools for Windows> cdb -server tcp:port=1025 -p 122
```

他のコンピューターでは、技術者は WinDbg をデバッグクライアントとして使用することを決定します。 次のコマンドを使用して開始できます。

```console
G:\Debugging Tools> windbg -remote tcp:server=BOX17,port=1025
```

別の例を示します。 この場合、NPIPE プロトコルが選択され、WinDbg ではなく CDB が使用されます。 最初のユーザーは、パイプ名を選択します。 これには、任意の英数字の文字列 (この例では "MainPipe") を指定できます。 最初のユーザーは、管理者特権でのコマンドプロンプトウィンドウ ([管理者として実行]) を開き、次のコマンドを入力してデバッグサーバーを起動します。

```console
E:\Debugging Tools for Windows> cdb -server npipe:pipe=MainPipe -v winmine.exe 
```

技術者は、サーバーコンピューターへのアクセス権を持たないアカウントでクライアントコンピューターにログオンしています。 しかし、この技術者は、サーバーコンピューターへのアクセス権を持つアカウントのユーザー名とパスワードを知っています。 そのアカウントのユーザー名は Contoso です。 技術者は次のコマンドを入力します。

```console
net use \\BOX17\ipc$ /user:Contoso
```

メッセージが表示されたら、技術者は Contoso アカウントのパスワードを入力します。

技術者は名前付きパイプに使用された名前がわからないので、使用可能なデバッグサーバーの BOX17 をクエリします。

```console
G:\Debugging Tools> cdb -QR \\BOX17
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

2つのパイプが表示されます。 ただし、1つだけがデバッグサーバーであり、もう1つはプロセスサーバーであり、それについては説明しません。 そのため、 **Mainpipe**は正しい名前である必要があります。 技術者は次のコマンドを使用して、デバッグクライアントを開始します。

```console
G:\Debugging Tools> cdb -remote npipe:server=BOX17,pipe=MyPipe 
```

### <a name="span-idusing_a_secure_serverspanspan-idusing_a_secure_serverspanusing-a-secure-server"></a><span id="using_a_secure_server"></span><span id="USING_A_SECURE_SERVER"></span>セキュリティで保護されたサーバーの使用

セキュリティで保護されたサーバーの例を次に示します。 このサーバーは、TLS1 の S チャネルプロトコルで secure sockets layer を使用します。 デバッガーはコンピューターストアで証明書を検索します。 証明書は、16進数の拇印によって指定されます。

```console
D:\> cdb -server "ssl:proto=tls1,machuser=ab 38 f7 ae 13 20 ac da 05 14 65 60 30 83 7b 83 09 2c d2 34,port=1234" notepad.exe
```

 

 






---
title: クライアントとサーバーの例
description: クライアントとサーバーの例
ms.assetid: 78dea1c0-6e94-4980-8042-375f11386d53
keywords:
- 例として、デバッガーからのリモート デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04a03d207896a9a0b07a0ef8e0570c4ecdd17ced
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550917"
---
# <a name="client-and-server-examples"></a>クライアントとサーバーの例


## <span id="ddk_client_and_server_examples_dbg"></span><span id="DDK_CLIENT_AND_SERVER_EXAMPLES_DBG"></span>


1 人のユーザーがという名前のコンピューターでアプリケーションを実行するいると仮定 *\\ \\BOX17*します。 このアプリケーションには、問題が、デバッグの技術者が異なるサイトにあります。

最初のユーザー設定で CDB を使用して、デバッグ サーバー  *\\ \\BOX17*します。 対象のアプリケーションでは、122 のプロセス ID を持ちます。 1025 のソケットのポート番号を持つ、TCP プロトコルが選択されます。 管理者特権でコマンド プロンプト ウィンドウ (管理者として実行) で、次のコマンドを入力してサーバーが起動します。

```console
E:\Debugging Tools for Windows> cdb -server tcp:port=1025 -p 122
```

その他のコンピューターでデバッグのクライアントとして WinDbg を使用する、技術者を決定します。 このコマンドを使用して開始ができます。

```console
G:\Debugging Tools> windbg -remote tcp:server=BOX17,port=1025
```

別の例を次に示します。 この場合、NPIPE プロトコルを選択すると、および CDB は WinDbg の代わりに使用されます。 最初のユーザーは、パイプ名を選択します。 この例では、"MainPipe"--任意の英数字の文字列を入力できます。 最初のユーザーは、管理者特権でコマンド プロンプト ウィンドウ (管理者として実行) を開き、このコマンドを入力してデバッグ サーバーを開始します。

```console
E:\Debugging Tools for Windows> cdb -server npipe:pipe=MainPipe -v winmine.exe 
```

技術者がサーバー コンピューターへのアクセスがないアカウントを使用してクライアント コンピューターにログオンします。 技術者は、ユーザー名とサーバー コンピューターへのアクセスがアカウントのパスワードを知っています。 そのアカウントのユーザー名は、Contoso です。 技術者は、次のコマンドを入力します。

```console
net use \\BOX17\ipc$ /user:Contoso
```

入力を求められたら、技術者は Contoso アカウントのパスワードを入力します。

技術者が把握していないため、彼女の BOX17 クエリを使用可能なデバッグ サーバーの名前付きパイプの名前が使用されました。

```console
G:\Debugging Tools> cdb -QR \\BOX17 
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

2 つのパイプが表示されます。 ただし、デバッグ サーバー--が 1 つだけ、もう一方は、プロセス サーバーは必要でないです。 したがって**MainPipe**正しい名前を指定する必要があります。 技術者は、デバッグのクライアントを開始するのに、次のコマンドを使用します。

```console
G:\Debugging Tools> cdb -remote npipe:server=BOX17,pipe=MyPipe 
```

### <a name="span-idusingasecureserverspanspan-idusingasecureserverspanusing-a-secure-server"></a><span id="using_a_secure_server"></span><span id="USING_A_SECURE_SERVER"></span>セキュリティで保護されたサーバーを使用します。

セキュリティで保護されたサーバーの例を次に示します。 このサーバーは、TLS1 のな S チャネル プロトコル、secure socket layer を使用します。 コンピューターのストアに証明書では、デバッガーが検索されます。 証明書は、16 進数、拇印によって指定されます。

```console
D:\> cdb -server "ssl:proto=tls1,machuser=ab 38 f7 ae 13 20 ac da 05 14 65 60 30 83 7b 83 09 2c d2 34,port=1234" notepad.exe
```

 

 






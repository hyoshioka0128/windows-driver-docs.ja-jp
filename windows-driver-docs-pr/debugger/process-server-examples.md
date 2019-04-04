---
title: プロセス サーバーの例
description: プロセス サーバーの例
ms.assetid: f87e6ff5-05a4-4dae-8151-913ea469b4ec
keywords:
- プロセス サーバー、例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dcd91d44f7883d5e4a75388f72304935ef13534
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551990"
---
# <a name="process-server-examples"></a>プロセス サーバーの例


## <span id="ddk_process_server_examples_dbg"></span><span id="DDK_PROCESS_SERVER_EXAMPLES_DBG"></span>


1 人のユーザーがという名前のコンピューターでアプリケーションを実行するいると仮定\\ \\BOX17 します。 このアプリケーションには、問題が、デバッグの技術者が異なるサイトにあります。

最初のユーザーの設定で DbgSrv を使用して、プロセス サーバーを\\ \\BOX17 します。 対象のアプリケーションでは、122 のプロセス ID を持ちます。 1025 のソケットのポート番号を持つ、TCP プロトコルが選択されます。 次のコマンドでサーバーが起動します。

```console
E:\Debugging Tools for Windows> dbgsrv -t tcp:port=1025 
```

その他のコンピューターでは、技術者は、このコマンドを使用してスマート クライアントとして WinDbg を起動します。

```console
G:\Debugging Tools> windbg -premote tcp:server=BOX17,port=1025 -p 122 
```

別の例を次に示します。 この場合、NPIPE プロトコルを選択すると、および CDB は WinDbg の代わりに使用されます。 最初のユーザーは、パイプ名を選択します。 この例では、"AnotherPipe"--任意の英数字の文字列を入力できます。 最初のユーザーは、管理者特権でコマンド プロンプト ウィンドウ (管理者として実行) を開き、このコマンドを入力してデバッグ サーバーを開始します。

```console
E:\Debugging Tools for Windows> dbgsrv -t npipe:pipe=AnotherPipe
```

技術者がサーバー コンピューターへのアクセスがないアカウントを使用してクライアント コンピューターにログオンします。 技術者は、ユーザー名とサーバー コンピューターへのアクセスがアカウントのパスワードを知っています。 そのアカウントのユーザー名は、Contoso です。 技術者は、次のコマンドを入力します。

```console
net use \\BOX17\ipc$ /user:Contoso
```

入力を求められたら、技術者は Contoso アカウントのパスワードを入力します。

技術者でないことを確認してプロセス サーバーの BOX17 をクエリしたため、どのような名前が使用される、名前付きパイプの。

```console
G:\Debugging Tools> cdb -QR \\BOX17 
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

2 つのパイプが表示されます。 ただし、プロセス サーバーでは--が 1 つだけ、もう一方はデバッグ サーバーの場合とは必要でないです。 したがって**AnotherPipe**正しい名前を指定する必要があります。 技術者は、スマート クライアントを起動するには、次のコマンドを入力します。

```console
G:\Debugging Tools> cdb -premote npipe:server=BOX17,pipe=AnotherPipe -v sol.exe 
```

複雑な例では、プロセス サーバーを使用して、[途中でシンボル](symbols-in-the-middle.md)を参照してください。

 

 






---
title: プロセス サーバーの例
description: プロセス サーバーの例
ms.assetid: f87e6ff5-05a4-4dae-8151-913ea469b4ec
keywords:
- プロセスサーバー, 例
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6d1e4618071c9b407aa5b75f16b9bf828ae12dc1
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563160"
---
# <a name="process-server-examples"></a>プロセス サーバーの例

たとえば、あるユーザーが BOX17 という名前のコンピューターでアプリケーションを実行していると \\ \\ します。 このアプリケーションには問題がありますが、デバッグ技術者は別のサイトにあります。

最初のユーザーは、BOX17 で DbgSrv を使用してプロセスサーバーを設定し \\ \\ ます。 ターゲットアプリケーションのプロセス ID は122です。 TCP プロトコルが選択されており、ソケットポート番号は1025です。 サーバーは、次のコマンドを使用して起動されます。

```console
E:\Debugging Tools for Windows> dbgsrv -t tcp:port=1025 
```

他のコンピューターでは、次のコマンドを使用して、テクニシャンがスマートクライアントとして WinDbg を起動します。

```console
G:\Debugging Tools> windbg -premote tcp:server=BOX17,port=1025 -p 122 
```

別の例を示します。 この場合、NPIPE プロトコルが選択され、WinDbg ではなく CDB が使用されます。 最初のユーザーは、パイプ名を選択します。 これには、任意の英数字の文字列 (この例では "その他のパイプ") を指定できます。 最初のユーザーは、管理者特権でのコマンドプロンプトウィンドウ ([管理者として実行]) を開き、次のコマンドを入力してデバッグサーバーを起動します。

```console
E:\Debugging Tools for Windows> dbgsrv -t npipe:pipe=AnotherPipe
```

技術者は、サーバーコンピューターへのアクセス権を持たないアカウントでクライアントコンピューターにログオンしています。 しかし、この技術者は、サーバーコンピューターへのアクセス権を持つアカウントのユーザー名とパスワードを知っています。 そのアカウントのユーザー名は Contoso です。 技術者は次のコマンドを入力します。

```console
net use \\BOX17\ipc$ /user:Contoso
```

メッセージが表示されたら、技術者は Contoso アカウントのパスワードを入力します。

技術者は名前付きパイプに使用された名前を確認できないので、プロセスサーバーの BOX17 をクエリします。

```console
G:\Debugging Tools> cdb -QR \\BOX17
Servers on \\BOX17:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
```

2つのパイプが表示されます。 ただし、プロセスサーバーは1つだけであり、もう一方はデバッグサーバーです。これについては説明しません。 そのため、他の**パイプ**は正しい名前である必要があります。 技術者は次のコマンドを入力して、スマートクライアントを起動します。

```console
G:\Debugging Tools> cdb -premote npipe:server=BOX17,pipe=AnotherPipe -v sol.exe
```

プロセスサーバーを使用したより複雑な例については、「[中間のシンボル](symbols-in-the-middle.md)」を参照してください。

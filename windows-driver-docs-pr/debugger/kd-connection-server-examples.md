---
title: KD 接続サーバーの例
description: KD 接続サーバーの例
ms.assetid: 5e54dda7-4f79-40e3-bcc5-248a3a047e31
keywords:
- KD 接続サーバー、例
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: e615d9467209b489b2e9be503318401ef71817e2
ms.sourcegitcommit: 8097a09d2f989a9b3dca250c4e2ffd4cec2172e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84563174"
---
# <a name="kd-connection-server-examples"></a>KD 接続サーバーの例


## <span id="ddk_kd_connection_server_examples_dbg"></span><span id="DDK_KD_CONNECTION_SERVER_EXAMPLES_DBG"></span>


デバッグするコンピューターが配置されているサイトにデバッグ技術者が存在しないとします。 デバッグ技術者は、このサイトのユーザーに対して、デバッグケーブルを使用してこのターゲットコンピューターを他のコンピューターに接続するように要求します。

この他のコンピューターは、IP アドレス127.0.0.42 に配置します。 デバッグケーブルは、このコンピューター上の COM1 を、ターゲットコンピューターでデバッグが有効になっているポートに接続します。 KD 接続サーバーは、次のコマンドを使用して開始されます。

```console
E:\Debugging Tools for Windows> kdsrv -t tcp:port=1027
```

次に、次のコマンドを使用して、技術者が WinDbg をスマートクライアントとして起動します。

```console
G:\Debugging Tools> windbg -k kdsrv:server=@{tcp:server=127.0.0.42,port=1027},trans=@{com:port=com1,baud=57600} -y SymbolPath
```

シンボルパスは、スマートクライアントが実行されているコンピューターに対する相対パスです。

別の例を示します。 この場合、NPIPE プロトコルが選択され、WinDbg ではなく KD が使用されます。 最初のユーザーは、パイプ名を選択します。 これには、任意の英数字の文字列を指定できます。この例では、"カーネルパイプ" です。 最初のユーザーは、管理者特権でのコマンドプロンプトウィンドウ ([管理者として実行]) を開き、次のコマンドを入力してデバッグサーバーを起動します。

```console
E:\Debugging Tools for Windows> set _NT_DEBUG_PORT=com1
E:\Debugging Tools for Windows> kdsrv -t npipe:pipe=KernelPipe
```

技術者は、サーバーコンピューターへのアクセス権を持たないアカウントでクライアントコンピューターにログオンしています。 しかし、この技術者は、サーバーコンピューターへのアクセス権を持つアカウントのユーザー名とパスワードを知っています。 そのアカウントのユーザー名は Contoso です。 技術者は次のコマンドを入力します。

```console
net use \\BOX17\ipc$ /user:Contoso
```

メッセージが表示されたら、技術者は Contoso アカウントのパスワードを入力します。

技術者は名前付きパイプに使用された名前を確認できないので、KD 接続サーバーの127.0.0.42 をクエリします。

```console
G:\Debugging Tools> cdb -QR 127.0.0.42
Servers on 127.0.0.42:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
Remote Kernel Debugger Server - npipe:Pipe=KernelPipe
```

3つのパイプが表示されます。 ただし、1つだけが KD 接続サーバーであり、それ以外は、デバッグサーバーとユーザーモードプロセスサーバーです。 技術者は次のコマンドを入力して、スマートクライアントを起動します。

```console
G:\Debugging Tools> kd -k kdsrv:server=@{npipe:server=127.0.0.42,pipe=KernelPipe},trans=@{com:baud=57600} -y SymbolPath
```

ボーレートが指定されているにもかかわらず、ポートが指定されていないことに注意してください。 これにより、デバッガーは、 \_ \_ KdSrv が実行されているコンピューターの NT デバッグポートによって指定されたポートに既定値を設定し \_ ます。

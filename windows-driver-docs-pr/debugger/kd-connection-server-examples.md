---
title: KD 接続サーバーの例
description: KD 接続サーバーの例
ms.assetid: 5e54dda7-4f79-40e3-bcc5-248a3a047e31
keywords:
- KD 接続のサーバー、例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e3e4e7a0a0c87a50c742c614f74acce2b32d8f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367426"
---
# <a name="kd-connection-server-examples"></a>KD 接続サーバーの例


## <span id="ddk_kd_connection_server_examples_dbg"></span><span id="DDK_KD_CONNECTION_SERVER_EXAMPLES_DBG"></span>


デバッグするコンピューターが配置されているサイトでは、デバッグの技術者が存在しないとします。 デバッグの技術者には、デバッグ ケーブルを使用して他のコンピューターにこの対象のコンピューターを接続するには、このサイトでだれかが求められます。

この他のコンピューターが 127.0.0.42 の IP アドレスであることができます。 デバッグ ケーブルは、このどちらのポートは、ターゲット コンピューターでデバッグが有効にされたコンピューター上の COM1 を接続します。 このコマンドでは、KD 接続のサーバーが起動します。

```console
E:\Debugging Tools for Windows> kdsrv -t tcp:port=1027 
```

その他の場所にある、技術者が開始 WinDbg としてこのコマンドを使用してスマート クライアント。

```console
G:\Debugging Tools> windbg -k kdsrv:server=@{tcp:server=127.0.0.42,port=1027},trans=@{com:port=com1,baud=57600} -y SymbolPath 
```

シンボル パスは、スマート クライアントが実行されているコンピューターを基準になります。

別の例を示します。 この場合、NPIPE プロトコルを選択すると、および KD は WinDbg の代わりに使用されます。 最初のユーザーは、パイプ名を選択します。 この例では、"KernelPipe"--任意の英数字の文字列を入力できます。 最初のユーザーは、管理者特権でコマンド プロンプト ウィンドウ (管理者として実行) を開き、これらのコマンドを入力してデバッグ サーバーを開始します。

```console
E:\Debugging Tools for Windows> set _NT_DEBUG_PORT=com1 
E:\Debugging Tools for Windows> kdsrv -t npipe:pipe=KernelPipe 
```

技術者がサーバー コンピューターへのアクセスがないアカウントを使用してクライアント コンピューターにログオンします。 技術者は、ユーザー名とサーバー コンピューターへのアクセスがアカウントのパスワードを知っています。 そのアカウントのユーザー名は、Contoso です。 技術者は、次のコマンドを入力します。

```console
net use \\BOX17\ipc$ /user:Contoso
```

入力を求められたら、技術者は Contoso アカウントのパスワードを入力します。

技術者でないことを確認して 127.0.0.42 KD 接続のサーバーのユーザー クエリを実行するため、どのような名前が使用される、名前付きパイプの。

```console
G:\Debugging Tools> cdb -QR 127.0.0.42 
Servers on 127.0.0.42:
Debugger Server - npipe:Pipe=MainPipe
Remote Process Server - npipe:Pipe=AnotherPipe
Remote Kernel Debugger Server - npipe:Pipe=KernelPipe
```

次の 3 つのパイプが表示されます。 ただし、KD 接続サーバーでは--が 1 つだけ、他のユーザーがデバッグ サーバーとユーザー モード プロセス サーバーです。 技術者は、スマート クライアントを開始する、次のコマンドは入力されます。

```console
G:\Debugging Tools> kd -k kdsrv:server=@{npipe:server=127.0.0.42,pipe=KernelPipe},trans=@{com:baud=57600} -y SymbolPath 
```

ボー レートが指定されてくださいが、ポートがないことを確認します。 これにより、デバッガーの既定値で指定されたポートが\_NT\_デバッグ\_KdSrv が実行されているコンピューターのポート。

 

 






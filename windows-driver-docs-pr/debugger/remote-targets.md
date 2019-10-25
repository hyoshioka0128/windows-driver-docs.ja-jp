---
title: リモート ターゲット
description: リモート ターゲット
ms.assetid: ed7ea3dc-07d1-481c-90e0-7f0b0e77ad42
keywords:
- デバッガーエンジン API, ターゲット, リモート
- デバッガーエンジン API, サーバーのデバッグ
- デバッガーエンジン API, プロセスサーバー
- デバッガーエンジン API, カーネル接続サーバー
- デバッガーエンジン API, スマートクライアント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d300432ea025610b3592ac767e1083fd3573daee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834285"
---
# <a name="remote-targets"></a>リモート ターゲット


## <span id="ddk_remote_debugging_dbx"></span><span id="DDK_REMOTE_DEBUGGING_DBX"></span>


リモートデバッグには、どのコンピューター (リモートクライアントまたはサーバー) がホストコンピューターであるかによって、2つの異なる形式があります。 *ホストコンピューター*は、[デバッガーエンジン](introduction.md#debugger-engine)がアクティブになっているコンピューターです。 その他のコンピューターでは、デバッガーエンジンは、ホストエンジンに対してコマンドとデータをリレーするプロキシとしてのみ機能します。

コマンドと[拡張機能](introduction.md#extensions)の実行やシンボルの読み込みなど、すべてのデバッガー操作は、ホストエンジンによって実行されます。 デバッガーセッションは、ホストエンジンに対する相対パスでもあります。

コンピューターで現在実行されているデバッグサーバーとプロセスサーバーを一覧表示するには、 [**Outputservers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-outputservers)を使用します。

### <a name="span-iddebugging_server_and_debugging_clientspanspan-iddebugging_server_and_debugging_clientspandebugging-servers-and-debugging-clients"></a><span id="debugging_server_and_debugging_client"></span><span id="DEBUGGING_SERVER_AND_DEBUGGING_CLIENT"></span>サーバーのデバッグとクライアントのデバッグ

*デバッグサーバー*は、ホストとして機能し、クライアントからの接続をリッスンするデバッガーエンジンのインスタンスです。 [**Startserver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-startserver)メソッドは、デバッグクライアントからの接続のリッスンを開始するようにデバッガーエンジンに指示します。

*デバッグクライアント*は、プロキシとして機能するデバッガーエンジンのインスタンスであり、デバッガーのコマンドと i/o をデバッグサーバーに送信します。 関数[**Debugconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)を使用して、デバッグサーバーに接続できます。

**Debugconnect**によって返されたクライアントオブジェクトは、デバッグサーバーのデバッガーセッションに自動的に結合されません。 メソッド[**Connectsession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-connectsession)を使用してセッションに参加し、入力と出力を同期できます。

デバッグサーバーとデバッグクライアントの間の通信は、多くの場合、サーバーに送信されたデバッガーコマンドと RPC 呼び出しと、クライアントに送信されたコマンド出力で構成されます。

### <a name="span-idprocess_server_and_smart_clientspanspan-idprocess_server_and_smart_clientspanprocess-servers-kernel-connection-servers-and-smart-clients"></a><span id="process_server_and_smart_client"></span><span id="PROCESS_SERVER_AND_SMART_CLIENT"></span>プロセスサーバー、カーネル接続サーバー、およびスマートクライアント

*プロセスサーバー*と*カーネル接続サーバー*は両方とも、プロキシとして機能するデバッガーエンジンのインスタンスであり、スマートクライアントからの接続をリッスンし、次のように要求されたメモリ、プロセッサ、またはオペレーティングシステムの操作を実行します。リモートクライアント。 *プロセスサーバー*は、同じコンピューター上で実行されているプロセスのデバッグを容易にします。 *カーネル接続サーバー*は、接続サーバーを実行しているコンピューターに接続されている Windows カーネルデバッグターゲットのデバッグを容易にします。 プロセスサーバーを開始するには、 [**StartProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-startprocessserver)またはプログラムの[dbgsrv](process-servers--user-mode-.md)を使用します。 [**Waitforprocessserverend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-waitforprocessserverend)メソッドは、 **StartProcessServer**によるプロセスサーバーの開始を待機します。 カーネル接続サーバーは、プログラム[**Kdsrv**](activating-a-kd-connection-server.md)を使用してアクティブ化できます。

*スマートクライアント*は、ホストエンジンとして機能し、プロセスサーバーに接続されているデバッガーエンジンのインスタンスです。 [**ConnectProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-connectprocessserver)メソッドはプロセスサーバーに接続します。 接続されたら、 [Live User Mode ターゲット](live-user-mode-targets.md)で説明されている方法を使用できます。

リモートクライアントがプロセスサーバーで終了した場合、 [**DisconnectProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-disconnectprocessserver)を使用して切断できます。または、 [**EndProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-endprocessserver)を使用してプロセスサーバーをシャットダウンするように要求することもできます。 プロセスサーバーを実行しているコンピューターからシャットダウンするには、タスクマネージャーを使用してプロセスを終了します。 **StartProcessServer**を使用したデバッガーエンジンのインスタンスがまだ実行中の場合は、 [**Execute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-execute)を使用してデバッガーコマンドを発行でき[**ます。 endsrv 0**](-endsrv--end-debugging-server-.md)はプロセスサーバーを終了します (これはの通常の動作の例外です **)。endsrv**。通常、プロセスサーバーには影響しません。

プロセスサーバーとスマートクライアントの間の通信は、通常、低レベルのメモリ、プロセッサ、およびオペレーティングシステムの操作と、リモートクライアントからサーバーに送信される要求で構成されます。 その結果がクライアントに返されます。

 

 






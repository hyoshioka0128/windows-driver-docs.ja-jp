---
title: リモート ターゲット
description: リモート ターゲット
ms.assetid: ed7ea3dc-07d1-481c-90e0-7f0b0e77ad42
keywords:
- エンジン API、ターゲット、リモートをデバッガーします。
- サーバーをデバッグするデバッガー エンジン API
- デバッガー エンジン API、プロセス サーバー
- デバッガー エンジン API、カーネル接続サーバー
- デバッガーのエンジンの API、スマート クライアント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327b6cce952b4e8c5eb1a94ef21a89bfb5061fc3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366416"
---
# <a name="remote-targets"></a>リモート ターゲット


## <span id="ddk_remote_debugging_dbx"></span><span id="DDK_REMOTE_DEBUGGING_DBX"></span>


コンピューター (リモート クライアントまたはサーバー) によって、ホスト コンピューターは、2 つのさまざまな形式のリモート デバッグなどがあります。 *ホスト コンピューター*いるコンピューターには、[デバッガー エンジン](introduction.md#debugger-engine)がアクティブです。 その他のコンピューターには、コマンドやホスト エンジンにデータを中継プロキシとしてデバッガー エンジンが機能しているだけです。

すべてのデバッガー コマンドを実行するなどの操作と[拡張](introduction.md#extensions)、およびシンボルの読み込み - ホスト エンジンによって実行されます。 デバッガー セッションは、ホストのエンジンを基準もあります。

デバッグ サーバーとコンピューターで現在実行中のプロセス サーバーを一覧表示するには使用[ **OutputServers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-outputservers)します。

### <a name="span-iddebuggingserveranddebuggingclientspanspan-iddebuggingserveranddebuggingclientspandebugging-servers-and-debugging-clients"></a><span id="debugging_server_and_debugging_client"></span><span id="DEBUGGING_SERVER_AND_DEBUGGING_CLIENT"></span>サーバーのデバッグとクライアントのデバッグ

A*サーバー デバッグ*デバッグ クライアントからの接続をリッスンしているホストとして機能するデバッガー エンジンのインスタンスです。 メソッド[**スタートサーバ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-startserver)デバッグ クライアントからの接続のリッスンを開始するデバッガー エンジンに指示されます。

A*デバッグ クライアント*デバッグ サーバーにデバッガー コマンドと I/O を送信し、プロキシとして機能するデバッガー エンジンのインスタンスです。 関数は、 [ **DebugConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugconnect)デバッグ サーバーへの接続に使用できます。

によって返されるクライアント オブジェクト**DebugConnect**デバッグ サーバー上のデバッガー セッションに自動的に参加していません。 メソッド[ **ConnectSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-connectsession)入力し、出力の同期セッションに参加させることができます。

デバッグ サーバーとデバッグのクライアント間の通信はほとんどの場合、デバッガー コマンドとコマンドの出力をクライアントに送信される、サーバーに送信された RPC 呼び出しで構成されます。

### <a name="span-idprocessserverandsmartclientspanspan-idprocessserverandsmartclientspanprocess-servers-kernel-connection-servers-and-smart-clients"></a><span id="process_server_and_smart_client"></span><span id="PROCESS_SERVER_AND_SMART_CLIENT"></span>プロセス サーバー、カーネルの接続のサーバー、およびスマート クライアント

*プロセス サーバー*と*カーネル接続サーバー*スマート クライアントからの接続をリッスンし、メモリ、プロセッサ、またはオペレーティング システムを実行するときに、プロキシとして機能するデバッガー エンジンの両方のインスタンスにはこれらのリモート クライアントからの要求での操作です。 A*プロセス サーバー*同じコンピューターで実行されているプロセスのデバッグが容易になります。 A*カーネル接続サーバー*接続サーバーを実行しているコンピューターに接続されているターゲットをデバッグする Windows カーネルのデバッグを容易にします。 メソッドを使用してプロセス サーバーを起動する[ **StartProcessServer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-startprocessserver)またはプログラム[DbgSrv](process-servers--user-mode-.md)します。 メソッド[ **WaitForProcessServerEnd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-waitforprocessserverend)のプロセス サーバーを使い始めるが待機**StartProcessServer**を終了します。 プログラムを使用してカーネルは、接続サーバーをアクティブにできる[ **KdSrv**](activating-a-kd-connection-server.md)します。

A*スマート クライアント*ホスト エンジンとして機能するデバッガー エンジンのインスタンスは、プロセス サーバーに接続します。 メソッド[ **ConnectProcessServer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-connectprocessserver)がプロセス サーバーに接続します。 接続したらで説明したメソッド[Live ユーザー モード ターゲット](live-user-mode-targets.md)ことができます。

使用してが切断できるリモート クライアントのプロセス サーバーと完了時に、 [ **DisconnectProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-disconnectprocessserver)を使用して[ **EndProcessServer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-endprocessserver)をプロセス サーバーのシャット ダウンを要求します。 実行されているコンピューターからプロセス サーバーをシャット ダウン、タスク マネージャーを使用して、プロセスを終了します。 デバッガーのインスタンスをエンジンを使用する場合**StartProcessServer**まだ実行中で使用できる[ **Execute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-execute)デバッガー コマンドを発行する[ **.endsrv 0**](-endsrv--end-debugging-server-.md)、プロセス サーバーが終了する (これは、通常の動作に例外 **.endsrv**、一般に影響しないプロセス サーバー)。

プロセス サーバーとスマート クライアント間の通信は通常、メモリ、プロセッサ、およびオペレーティング システムの低レベルの操作とリモート クライアントからサーバーに送信される要求で構成されます。 その結果、クライアントに送信されます。

 

 






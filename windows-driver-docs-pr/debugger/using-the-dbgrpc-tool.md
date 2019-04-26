---
title: DbgRpc ツールの使用
description: DbgRpc ツールの使用
ms.assetid: a98b9141-72e1-4957-a65c-36e677d159a6
keywords:
- DbgRpc
- させるため、基本的な使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18926641104455df4d8804af9f21ddc0b458cbf3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340544"
---
# <a name="using-the-dbgrpc-tool"></a>DbgRpc ツールの使用


## <span id="ddk_using_the_dbgrpc_tool_dbg"></span><span id="DDK_USING_THE_DBGRPC_TOOL_DBG"></span>


させるためのツール (Dbgrpc.exe) の Windows 内のデバッグ ツールのインストールのルート ディレクトリにあるし、コマンド プロンプト ウィンドウで開始する必要があります。 アイコンをダブルクリックしても、このツールは開始されません。

コマンド プロンプト ウィンドウは、ローカル コンピューターでは、管理者特権を持つ、またはドメイン管理者特権を持つアカウントで実行する必要があります。

させるためには、すべてのシステム サービス (LSASS) などの呼び出しがありません。 これにより、カーネルがまだ実行されている限り場合でも、システム サービスがクラッシュのデバッグに役立ちます。

### <a name="span-idusingdbgrpconaremotecomputerspanspan-idusingdbgrpconaremotecomputerspanusing-dbgrpc-on-a-remote-computer"></a><span id="using_dbgrpc_on_a_remote_computer"></span><span id="USING_DBGRPC_ON_A_REMOTE_COMPUTER"></span>リモート コンピューター上のさせるための使用

させるためがリモート コンピューターから情報を調べることもできます。 これを機能させるには、リモート コンピューターをリモート接続を受け入れるし、リモート ユーザーを認証することにある必要があります。 場合は、リモート コンピューターの RPCSS (RPC エンドポイント マッパー) サービスがクラッシュすると、させるためは使用できません。 リモート コンピューター上の管理またはドメインの管理者特権が必要です。

**-S**サーバー名を指定するコマンド ライン オプションを使用し、 **-p**トランスポート プロトコルを指定するパラメーターを使用します。 TCP と名前付きパイプ プロトコルの両方があります。 TCP は、推奨されるプロトコルです。これは、ほぼすべての状況で動作します。

以下に例を示します。

```console
G:\>dbgrpc -s MyServer -p ncacn_ip_tcp -l -P 1e8 -L 0.1
Getting remote cell info ...
Endpoint
Status: Active
Protocol Sequence: LRPC
Endpoint name: OLE18
```

### <a name="span-iddbgrpccommandlinespanspan-iddbgrpccommandlinespandbgrpc-command-line"></a><span id="dbgrpc_command_line"></span><span id="DBGRPC_COMMAND_LINE"></span>させるためのコマンドライン

完全なコマンド構文については、次を参照してください。 [**させるためのコマンド ライン オプション**](dbgrpc-command-line-options.md)します。

 

 






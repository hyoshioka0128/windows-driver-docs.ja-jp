---
title: RPC エンドポイント情報の取得
description: RPC エンドポイント情報の取得
ms.assetid: 8e852855-896c-4553-8a58-8ca49c7b2e0a
keywords:
- RPC エンドポイント情報
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1d37305e12f731a46178ce9b919ecc8482ec8ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379448"
---
# <a name="get-rpc-endpoint-information"></a>RPC エンドポイント情報の取得


## <span id="ddk_get_rpc_endpoint_information_dbg"></span><span id="DDK_GET_RPC_ENDPOINT_INFORMATION_DBG"></span>


エンドポイント情報を表示、 **! rpcexts.getendpointinfo**拡張機能、またはさせるためと、 **-e**スイッチを使用します。

エンドポイントの数が指定されている場合は、そのエンドポイントに関する情報が表示されます。 省略した場合、システム上のすべてのプロセスのエンドポイントが表示されます。

次の例では、すべてのエンドポイントが表示されます。 これは、多くの場合、プロセス Id を取得し、その他のコマンドの引数として使用できる数値をセルに便利な方法です。

```console
D:\wmsg>dbgrpc -e
Searching for endpoint info ...
## PID  CELL ID   ST PROTSEQ        ENDPOINT
-------------------------------------------------------
00a8 0000.0001 01            NMP \PIPE\InitShutdown
00a8 0000.0003 01            NMP \PIPE\SfcApi
00a8 0000.0004 01            NMP \PIPE\ProfMapApi
00a8 0000.0007 01            NMP \pipe\winlogonrpc
00a8 0000.0008 01           LRPC OLE5
00c4 0000.0001 01           LRPC ntsvcs
00c4 0000.0003 01            NMP \PIPE\ntsvcs
00c4 0000.0008 01            NMP \PIPE\scerpc
00d0 0000.0001 01            NMP \PIPE\lsass
00d0 0000.0004 01            NMP \pipe\WMIEP_d0
00d0 0000.000b 01            NMP \PIPE\POLICYAGENT
00d0 0000.000c 01           LRPC policyagent
0170 0000.0001 01           LRPC epmapper
0170 0000.0003 01            TCP 135
0170 0000.0005 01            SPX 34280
0170 0000.0006 01             NB 135
0170 0000.0007 01             NB 135
0170 0000.000b 01            NMP \pipe\epmapper
01b8 0000.0001 01            NMP \pipe\spoolss
01b8 0000.0003 01           LRPC spoolss
01b8 0000.0007 01           LRPC OLE7
00ec 0000.0001 01           LRPC OLE2
00ec 0000.0003 01           LRPC senssvc
00ec 0000.0007 01            NMP \pipe\tapsrv
00ec 0000.0008 01           LRPC tapsrvlpc
00ec 0000.000c 01            NMP \PIPE\ROUTER
00ec 0000.0010 01            NMP \pipe\WMIEP_ec
0214 0000.0001 01            NMP \PIPE\winreg
022c 0000.0001 01           LRPC LRPC0000022c.00000001
022c 0000.0003 01            TCP 1058
022c 0000.0005 01            SPX 24576
022c 0000.0006 01            NMP \PIPE\atsvc
02a8 0000.0001 01           LRPC OLE3
0370 0000.0001 01           LRPC OLE9
0278 0000.0001 01            TCP 1120
030c 0000.0001 01           LRPC OLE12
```

省略可能なパラメーターの詳細については、「 [**させるためのコマンド ライン オプション**](dbgrpc-command-line-options.md)します。

デバッガーの拡張機能の RPC を使用して類似の例については、「 [ **! rpcexts.getendpointinfo**](-rpcexts-getendpointinfo.md)します。

 

 






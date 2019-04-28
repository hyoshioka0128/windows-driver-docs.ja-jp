---
title: RPC クライアント呼び出し情報の取得
description: RPC クライアント呼び出し情報の取得
ms.assetid: 8b23428d-50e7-4613-a0ce-d1da5fa96ddf
keywords:
- RPC クライアント呼び出し情報
- CCALL (クライアントの呼び出し)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b2e89636c8be390a045341ea94de9ca4d43fd55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380196"
---
# <a name="get-rpc-client-call-information"></a>RPC クライアント呼び出し情報の取得


## <span id="ddk_get_rpc_client_call_information_dbg"></span><span id="DDK_GET_RPC_CLIENT_CALL_INFORMATION_DBG"></span>


クライアントの呼び出し (CCALL) 呼び出し情報を表示、 **! rpcexts.getclientcallinfo**拡張機能、またはさせるためときに、 **-** スイッチを使用します。

次の 4 つの省略可能なパラメーターが許可されます。 -これらの 3 つ*CallID*、 *IfStart*、および*ProcNum* --RPC の呼び出しを追跡するために使用する情報を識別します。 4 番目のパラメーターでは、 *ProcessID*は、呼び出しを所有するプロセスの pid を調べます。 検索を絞り込むことがわかっているパラメーターを指定する必要があります。

パラメーターが指定されていない場合は、システム内のすべての既知 CCALLs が表示されます。 この (可能性のある長い) の表示の例を次に示します。

```console
D:\wmsg>dbgrpc -a
Searching for call info ...
## PID  CELL ID   PNO  IFSTART  TIDNUMBER CALLID   LASTTIME PS CLTNUMBER ENDPOINT
------------------------------------------------------------------------------
0390 0000.0001 0000 19bb5061 0000.0000 00000001 00072bff 07 0000.0002 1120
```

省略可能なパラメーターの詳細については、「 [**させるためのコマンド ライン オプション**](dbgrpc-command-line-options.md)します。

デバッガーの拡張機能の RPC を使用して類似の例については、「 [ **! rpcexts.getclientcallinfo**](-rpcexts-getclientcallinfo.md)します。

**注**  場合にだけ、クライアントが呼び出すオブジェクトに関する情報が収集、**完全**状態情報が収集されています。 参照してください[RPC 状態情報を有効にする](enabling-rpc-state-information.md)詳細についてはします。

 

 

 






---
title: DbgRpc のコマンドライン オプション
description: させるためのコマンドラインは、常に-l、e、-t、- c、または-a スイッチの 1 つだけに含める必要があります。 これらのスイッチを次のオプションは、使用されるスイッチに依存します。
ms.assetid: 1c90f97c-f054-402d-a559-2459528029b9
keywords:
- させるためのコマンド ライン オプションの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbgRpc Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce281a846de1270482ae0e51840c62a388581b0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574573"
---
# <a name="dbgrpc-command-line-options"></a>DbgRpc のコマンドライン オプション


させるためのコマンドラインは、常に-l、e、-t、- c、または-a スイッチの 1 つだけに含める必要があります。 これらのスイッチを次のオプションは、使用されるスイッチに依存します。 -S、-p、および-r オプションは、その他のオプションで使用できます。

```console
 dbgrpc [-s Server -p ProtSeq] [-r Radix] -l -P ProcessID -L CellID1.CellID2 

dbgrpc [-s Server -p ProtSeq] [-r Radix] -e [-E EndpointName] 

dbgrpc [-s Server -p ProtSeq] [-r Radix] -t -P ProcessID [-T ThreadID] 

dbgrpc [-s Server -p ProtSeq] [-r Radix] [-c|-a] [-C CallID] [-I IfStart] [-N ProcNum] [-P ProcessID] 

dbgrpc -? 
```

## <a name="span-idddkdbgrpccommandlineoptionsdbgspanspan-idddkdbgrpccommandlineoptionsdbgspanparameters"></a><span id="ddk_dbgrpc_command_line_options_dbg"></span><span id="DDK_DBGRPC_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="_______-s_______Server______"></span><span id="_______-s_______server______"></span><span id="_______-S_______SERVER______"></span> **-s** *サーバー*   
リモート コンピューターから情報を表示させるために使用できます。 スラッシュ記号は、サーバー名にする必要があります前ありません。 リモートでさせるための使用に関する詳細については、次を参照してください。[させるためのツールを使用して](using-the-dbgrpc-tool.md)します。

<span id="_______-p_______ProtSeq______"></span><span id="_______-p_______protseq______"></span><span id="_______-P_______PROTSEQ______"></span> **-p** *ProtSeq*   
使用するリモートのトランスポートを指定します。 可能な値*ProtSeq*は**ncacn\_ip\_tcp** (TCP プロトコル) および**ncacn\_np** (名前付きパイプ プロトコル)。 TCP プロトコルをお勧めします。 リモートでさせるための使用に関する詳細については、次を参照してください。[させるためのツールを使用して](using-the-dbgrpc-tool.md)します。

<span id="_______-r_______Radix______"></span><span id="_______-r_______radix______"></span><span id="_______-R_______RADIX______"></span> **-r** *基数*   
コマンドのパラメーターに使用する基数を指定します。 既定値は、基数 16 です。 場合、 **-r**パラメーターを使用すると、配置する最初の行自体の後にリストされているパラメーターのみに影響するため、します。 させるためのツールの出力には影響しません。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
指定したセルの RPC 状態情報を表示します。 例については、次を参照してください。 [RPC セル情報の取得](get-rpc-cell-information.md)します。

<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *プロセス Id*   
プロセスのプロセス ID (PID) を指定します。 ときに、 **-l**オプションが使用されている、このアカウントは、プロセス サーバーが、目的のセルが含まれています。 ときに、 **-t**オプションが使用されている、目的のスレッドを格納しているプロセスがあります。 ときに、 **-c**または **-a**オプションが使用されている、このパラメーターは省略可能です。 サーバー プロセスを表示する呼び出しを所有している必要があります。

<span id="cellid1.cellid2______"></span><span id="CELLID1.CELLID2______"></span>*CellID1*.*CellID2*   
表示するセルの数を指定します。

<span id="_______-e______"></span><span id="_______-E______"></span> **-e**   
エンドポイントは、システムの RPC 状態情報を検索します。 例については、次を参照してください。 [RPC エンドポイント情報の取得](get-rpc-endpoint-information.md)します。

<span id="_______EndpointName______"></span><span id="_______endpointname______"></span><span id="_______ENDPOINTNAME______"></span> *EndpointName*   
表示されるエンドポイントの数を指定します。 省略した場合は、システム上のすべてのプロセスのエンドポイントが表示されます。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
スレッドは、システムの RPC 状態情報を検索します。 例については、次を参照してください。 [RPC スレッド情報の取得](get-rpc-thread-information.md)します。

<span id="_______ThreadID______"></span><span id="_______threadid______"></span><span id="_______THREADID______"></span> *ThreadID*   
表示されるスレッドのスレッド ID を指定します。 省略した場合、指定されたプロセスのすべてのスレッドが表示されます。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
検索サーバー側のシステムの RPC 状態情報は、(SCALL) 情報を呼び出します。 例については、次を参照してください。 [RPC 呼び出し情報の取得](get-rpc-call-information.md)します。

<span id="_______-a______"></span><span id="_______-A______"></span> **-**   
検索システムの RPC 状態情報がクライアントでは、(CCALL) 情報を呼び出します。 例については、次を参照してください。 [RPC クライアント呼び出し情報の取得](get-rpc-client-call-information.md)します。 このオプションでは、完全な RPC 状態情報が必要です。

<span id="_______CallID______"></span><span id="_______callid______"></span><span id="_______CALLID______"></span> *CallID*   
呼び出し ID を指定します このパラメーターは省略可能です。呼び出し、特定の一致を表示する場合にのみに*CallID*値。

<span id="_______IfStart______"></span><span id="_______ifstart______"></span><span id="_______IFSTART______"></span> *IfStart*   
呼び出しが行われたは、インターフェイスの汎用一意識別子 (UUID) の最初の dword 値を指定します。 このパラメーターは省略可能です。呼び出し、特定の一致を表示する場合にのみに*IfStart*値。

<span id="_______ProcNum______"></span><span id="_______procnum______"></span><span id="_______PROCNUM______"></span> *ProcNum*   
この呼び出しのプロシージャ番号を指定します。 (RPC ランタイムは、IDL ファイル内の位置番号でインターフェイスから個々 のルーチンを識別します。--インターフェイスの最初のルーチンは、0 と 2 つ目の 1)。このパラメーターは省略可能です。呼び出し、特定の一致を表示する場合にのみに*ProcNum*値。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Microsoft リモート プロシージャ コール (RPC) のデバッグの詳細については、次を参照してください。 [RPC デバッグ](rpc-debugging.md)します。

 

 






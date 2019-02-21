---
title: rpcexts.getendpointinfo
description: Rpcexts.getendpointinfo 拡張機能は、エンドポイントは、システムの RPC 状態情報を検索します。
ms.assetid: 3efd0cd1-bcdd-4785-aa00-a32a7578219c
keywords:
- デバッグ rpcexts.getendpointinfo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getendpointinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 732c769f3c9636269576edb88f64762864b8f6c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559968"
---
# <a name="rpcextsgetendpointinfo"></a>!rpcexts.getendpointinfo


**! Rpcexts.getendpointinfo**拡張機能は、エンドポイントは、システムの RPC 状態情報を検索します。

```dbgcmd
    !rpcexts.getendpointinfo [EndpointName] 
!rpcexts.getendpointinfo -? 
```

## <a name="span-idddkrpcextsgetendpointinfodbgspanspan-idddkrpcextsgetendpointinfodbgspanparameters"></a><span id="ddk__rpcexts_getendpointinfo_dbg"></span><span id="DDK__RPCEXTS_GETENDPOINTINFO_DBG"></span>パラメーター


<span id="_______EndpointName______"></span><span id="_______endpointname______"></span><span id="_______ENDPOINTNAME______"></span> *EndpointName*   
表示されるエンドポイントの数を指定します。 省略した場合は、システム上のすべてのプロセスのエンドポイントが表示されます。

<span id="_______-_______"></span> **-?**   
コマンド プロンプト ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Microsoft リモート プロシージャ コール (RPC) のデバッグの詳細については、次を参照してください。 [RPC デバッグ](rpc-debugging.md)します。

<a name="remarks"></a>注釈
-------

この拡張機能は、CDB と WinDbg のユーザー モードにのみ使用できます。

以下に例を示します。

```dbgcmd
0:002> !rpcexts.getendpointinfo
Searching for endpoint info ...
## PID  CELL ID   ST PROTSEQ        ENDPOINT
-------------------------------------------------------------
00a8 0000.0001 01            NMP \PIPE\InitShutdown
00a8 0000.0003 01            NMP \PIPE\SfcApi
00a8 0000.0004 01            NMP \PIPE\ProfMapApi
00a8 0000.0005 01           LRPC OLE5
00a8 0000.0007 01            NMP \pipe\winlogonrpc
00c4 0000.0001 01           LRPC ntsvcs
00c4 0000.0003 01            NMP \PIPE\ntsvcs
00c4 0000.0008 01            NMP \PIPE\scerpc
00d0 0000.0001 01            NMP \PIPE\lsass
00d0 0000.0003 01            NMP \pipe\WMIEP_d0
00d0 0000.0006 01           LRPC policyagent
00d0 0000.0007 01            NMP \PIPE\POLICYAGENT
0170 0000.0001 01           LRPC epmapper
0170 0000.0003 01            TCP 135
0170 0000.0005 01            SPX 34280
0170 0000.0006 01             NB 135
0170 0000.0007 01             NB 135
0170 0000.000b 01            NMP \pipe\epmapper
01c0 0000.0001 01            NMP \pipe\spoolss
01c0 0000.0003 01           LRPC spoolss
01c0 0000.0007 01           LRPC OLE7
020c 0000.0001 01           LRPC OLE2
020c 0000.0005 01           LRPC senssvc
020c 0000.0007 01            NMP \pipe\tapsrv
020c 0000.0009 01           LRPC tapsrvlpc
020c 0000.000c 01            NMP \PIPE\ROUTER
020c 0000.0016 01            NMP \pipe\WMIEP_20c
0218 0000.0001 01            NMP \PIPE\winreg
022c 0000.0001 01           LRPC LRPC0000022c.00000001
022c 0000.0003 01            TCP 1041
022c 0000.0005 01            SPX 24576
022c 0000.0006 01            NMP \PIPE\atsvc
0294 0000.0001 01           LRPC OLE3
0378 0000.0001 01           LRPC OLE9
026c 0000.0001 01            TCP 1118
0344 0000.0001 01           LRPC OLE12
```

させるためのツールを使用して同様の例を参照してください。 [RPC エンドポイント情報の取得](get-rpc-endpoint-information.md)します。

 

 






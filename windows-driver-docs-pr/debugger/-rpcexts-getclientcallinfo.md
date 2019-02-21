---
title: rpcexts.getclientcallinfo
description: Rpcexts.getclientcallinfo 拡張機能は、クライアントの呼び出し (CCALL) について、システムの RPC 状態情報を検索します。
ms.assetid: 1b838238-63b3-4618-bc59-6b4d74274b9c
keywords:
- rpcexts.getclientcallinfo Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getclientcallinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e14d7d01bedc1543b1303f8494324e38e36933da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552350"
---
# <a name="rpcextsgetclientcallinfo"></a>!rpcexts.getclientcallinfo


**! Rpcexts.getclientcallinfo**拡張機能は、クライアントの呼び出し (CCALL) について、システムの RPC 状態情報を検索します。

```dbgcmd
!rpcexts.getclientcallinfo [ CallID | 0 [ IfStart | 0 [ ProcNum | 0xFFFF [ProcessID|0] ] ] ] 
!rpcexts.getclientcallinfo -? 
```

## <a name="span-idddkrpcextsgetclientcallinfodbgspanspan-idddkrpcextsgetclientcallinfodbgspanparameters"></a><span id="ddk__rpcexts_getclientcallinfo_dbg"></span><span id="DDK__RPCEXTS_GETCLIENTCALLINFO_DBG"></span>パラメーター


<span id="_______CallID______"></span><span id="_______callid______"></span><span id="_______CALLID______"></span> *CallID*   
呼び出し ID を指定します このパラメーターは省略可能です。特定の一致する呼び出しを表示する場合に*CallID*値。

<span id="_______IfStart______"></span><span id="_______ifstart______"></span><span id="_______IFSTART______"></span> *IfStart*   
呼び出しが行われたインターフェイス UUID の最初の dword 値を指定します。 このパラメーターは省略可能です。特定の一致する呼び出しを表示する場合に*IfStart*値。

<span id="_______ProcNum______"></span><span id="_______procnum______"></span><span id="_______PROCNUM______"></span> *ProcNum*   
この呼び出しのプロシージャ番号を指定します。 (RPC ランタイムは、IDL ファイル内の位置番号でインターフェイスから個々 のルーチンを識別します。--インターフェイスの最初のルーチンは、0 と 2 つ目の 1)。このパラメーターは省略可能です。特定の一致する呼び出しを表示する場合に*ProcNum*値。

<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *プロセス Id*   
プロセスを表示する呼び出しを所有するクライアント プロセスの ID (PID) を指定します。 このパラメーターは省略可能です。複数のプロセスによって所有されている呼び出しを表示する場合は、これを省略します。

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

この拡張機能は、CDB と WinDbg のユーザー モードにのみ使用できます。 これは完全な RPC 状態情報が収集されている場合のみ使用できます。

以下に例を示します。

```dbgcmd
0:002> !rpcexts.getclientcallinfo
Searching for call info ...
## PID  CELL ID   PNO  IFSTART  TIDNUMBER CALLID   LASTTIME PS CLTNUMBER ENDPOINT
------------------------------------------------------------------------------
03d4 0000.0001 0000 19bb5061 0000.0000 00000001 0004ca9b 07 0000.0002 1118
```

させるためのツールを使用して同様の例を参照してください。 [RPC クライアント呼び出し情報の取得](get-rpc-client-call-information.md)します。

 

 






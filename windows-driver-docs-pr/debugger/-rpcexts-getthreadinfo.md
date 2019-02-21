---
title: rpcexts.getthreadinfo
description: Rpcexts.getthreadinfo 拡張機能は、スレッドは、システムの RPC 状態情報を検索します。
ms.assetid: 904605e7-c53b-4e29-874f-7a055fc7a02b
keywords:
- デバッグ rpcexts.getthreadinfo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getthreadinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff41bcd6c0440acac8105aeea45fcc5c63a4026f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529583"
---
# <a name="rpcextsgetthreadinfo"></a>!rpcexts.getthreadinfo


**! Rpcexts.getthreadinfo**拡張機能は、スレッドは、システムの RPC 状態情報を検索します。

```dbgcmd
!rpcexts.getthreadinfo ProcessID [ThreadID] 
!rpcexts.getthreadinfo -? 
```

## <a name="span-idddkrpcextsgetthreadinfodbgspanspan-idddkrpcextsgetthreadinfodbgspanparameters"></a><span id="ddk__rpcexts_getthreadinfo_dbg"></span><span id="DDK__RPCEXTS_GETTHREADINFO_DBG"></span>パラメーター


<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *プロセス Id*   
プロセスの目的のスレッドを格納しているプロセス ID (PID) を指定します。

<span id="_______ThreadID______"></span><span id="_______threadid______"></span><span id="_______THREADID______"></span> *ThreadID*   
表示されるスレッドのスレッド ID を指定します。 省略した場合、指定されたプロセスのすべてのスレッドが表示されます。

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
0:002> !rpcexts.getthreadinfo 26c
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
026c 0000.0002 01 000003c4 0004caa5
026c 0000.0005 03 00000254 0004ca9b
```

させるためのツールを使用して同様の例を参照してください。 [RPC スレッド情報の取得](get-rpc-thread-information.md)します。

 

 






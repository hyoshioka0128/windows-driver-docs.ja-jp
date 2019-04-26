---
title: rpcexts.getdbgcell
description: Rpcexts.getdbgcell 拡張機能には、指定したセルの RPC 状態情報が表示されます。
ms.assetid: 28be074f-6756-4610-aa86-1162b83fd0a7
keywords:
- デバッグ rpcexts.getdbgcell Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getdbgcell
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e95847021c0f8c860a3c55e875be357e9e3b3cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338864"
---
# <a name="rpcextsgetdbgcell"></a>!rpcexts.getdbgcell


**! Rpcexts.getdbgcell**拡張機能には、指定したセルの RPC 状態情報が表示されます。

```dbgcmd
!rpcexts.getdbgcell ProcessID CellID1.CellID2 
!rpcexts.getdbgcell -?
```

## <a name="span-idddkrpcextsgetdbgcelldbgspanspan-idddkrpcextsgetdbgcelldbgspanparameters"></a><span id="ddk__rpcexts_getdbgcell_dbg"></span><span id="DDK__RPCEXTS_GETDBGCELL_DBG"></span>パラメーター


<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span> *プロセス Id*   
プロセス サーバーが、目的のセルが含まれています、プロセスの ID (PID) を指定します。

<span id="_______cellid1.cellid2______"></span><span id="_______CELLID1.CELLID2______"></span> *CellID1*.*CellID2*   
表示するセルの数を指定します。

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
0:002> !rpcexts.getdbgcell c4 0.19
Getting cell info ...
Call
Status: Active
Procedure Number: 11
Interface UUID start (first DWORD only): 82273FDC
Call ID: 0x0 (0)
Servicing thread identifier: 0x0.3E
Call Flags: cached, LRPC
Last update time (in seconds since boot):1453.459 (0x5AD.1CB)
Caller (PID/TID) is: d0.1ac (208.428)
```

させるためのツールを使用して同様の例を参照してください。 [RPC セル情報の取得](get-rpc-cell-information.md)します。

 

 






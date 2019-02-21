---
title: rpcexts.thread
description: Rpcexts.thread 拡張機能は、スレッドごとの RPC の情報を表示します。この拡張機能のコマンドは、.thread コマンドと混同しないでください。
ms.assetid: eecc4eb6-7789-47ed-8b3f-5ec21cc6117c
keywords:
- デバッグ rpcexts.thread Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe1b069d044f2e5c518c7d3d91fe47613ffa94fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535446"
---
# <a name="rpcextsthread"></a>!rpcexts.thread


**! Rpcexts.thread**拡張機能には、スレッドごとの RPC 情報が表示されます。

この拡張機能のコマンドと混同しないで、 [ **.thread (登録コンテキストの設定)** ](-thread--set-register-context-.md)コマンドまたは[ **! スレッド**](-thread.md) (!kdextx86.thread と! kdexts.thread) 拡張機能。

```dbgcmd
!rpcexts.thread TEB
```

## <a name="span-idddkrpcextsthreaddbgspanspan-idddkrpcextsthreaddbgspanparameters"></a><span id="ddk__rpcexts_thread_dbg"></span><span id="DDK__RPCEXTS_THREAD_DBG"></span>パラメーター


<span id="_______TEB______"></span><span id="_______teb______"></span> *TEB*   
終了スレッド環境ブロックのアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
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

この拡張機能は、スレッドごとの RPC の情報を表示します。 スレッドごとの RPC 情報内のフィールドは、このスレッドの拡張エラー情報です。

以下に例を示します。

```dbgcmd
0:001> !rpcexts.thread 7ffdd000
RPC TLS at 692e70

HandleToThread - 0x6c
SavedProcedure - 0x0
SavedParameter - 0x0
ActiveCall - 0x0
Context - 0x0
CancelTimeout - 0xffffffff
SecurityContext - 0x0
ExtendedStatus - 0x0
ThreadEEInfo - 0xb015f0
ThreadEvent at - 0x00692E78
fCallCancelled - 0x0
buffer cache array at - 0x00692E84
fAsync - 0x0
```

 

 






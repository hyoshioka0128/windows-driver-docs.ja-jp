---
title: rpcexts.rpcreadstack
description: Rpcexts.rpcreadstack 拡張機能では、RPC クライアント側のスタックを読み取って呼び出し情報を取得します。
ms.assetid: e0988ac9-dc6e-4a4f-9096-6af2e70dcd42
keywords:
- デバッグ rpcexts.rpcreadstack Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.rpcreadstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b0f586e84621a94a5472151c447b115307869fd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570671"
---
# <a name="rpcextsrpcreadstack"></a>!rpcexts.rpcreadstack


**! Rpcexts.rpcreadstack**拡張機能が、RPC クライアント側のスタックを読み取り、呼び出し情報を取得します。

```dbgcmd
!rpcexts.rpcreadstack ThreadStackPointer
```

## <a name="span-idddkrpcextsrpcreadstackdbgspanspan-idddkrpcextsrpcreadstackdbgspanparameters"></a><span id="ddk__rpcexts_rpcreadstack_dbg"></span><span id="DDK__RPCEXTS_RPCREADSTACK_DBG"></span>パラメーター


<span id="_______ThreadStackPointer______"></span><span id="_______threadstackpointer______"></span><span id="_______THREADSTACKPOINTER______"></span> *ThreadStackPointer*   
スレッドのスタックへのポインターを指定します。

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

Microsoft リモート プロシージャ コール (RPC) のデバッグの詳細については、[RPC デバッグ](rpc-debugging.md)を参照してください。

<a name="remarks"></a>コメント
-------

この拡張機能の一般的な用途は、[呼び出しスタックしている問題を分析](analyzing-a-stuck-call-problem.md)を参照してください。

以下に例を示します。

```dbgcmd
0:001> !rpcexts.rpcreadstack 68fba4
CallID: 1
IfStart: 19bb5061
ProcNum: 0
        Protocol Sequence:      "ncacn_ip_tcp"  (Address: 00692ED8)
        NetworkAddress: ""      (Address: 00692F38)
        Endpoint:       "1120"  (Address: 00693988)
```

 

 






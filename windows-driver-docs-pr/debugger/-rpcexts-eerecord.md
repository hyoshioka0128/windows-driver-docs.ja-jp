---
title: rpcexts.eerecord
description: Rpcexts.eerecord 拡張機能には、拡張エラー情報のレコードの内容が表示されます。
ms.assetid: 3c861842-d3ac-4c7d-88e3-d00233189b74
keywords:
- デバッグ rpcexts.eerecord Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.eerecord
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10d9e9034609d1eb91f39b85422365ba9c9e6046
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582223"
---
# <a name="rpcextseerecord"></a>!rpcexts.eerecord


**! Rpcexts.eerecord**拡張機能の拡張エラー情報レコードの内容を表示します。

```dbgcmd
!rpcexts.eerecord EERecordAddress
```

## <a name="span-idddkrpcextseerecorddbgspanspan-idddkrpcextseerecorddbgspanparameters"></a><span id="ddk__rpcexts_eerecord_dbg"></span><span id="DDK__RPCEXTS_EERECORD_DBG"></span>パラメーター


<span id="_______EERecordAddress______"></span><span id="_______eerecordaddress______"></span><span id="_______EERECORDADDRESS______"></span> *EERecordAddress*   
拡張エラー レコードのアドレスを指定します。

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

<a name="remarks"></a>コメント
-------

この拡張機能には、デバッガーで拡張エラー情報の 1 つのレコードの内容が表示されます。 ほとんどの場合は使いやすい[ **! rpcexts.eeinfo**](-rpcexts-eeinfo.md)、チェーン全体が表示されます。 1 つのレコードを使用して、チェーンが非常に長い場合 **! eerecord**代わりにします。

以下に例を示します。

```dbgcmd
0:001> !rpcexts.eerecord 0xb015f0
Computer Name: (null)
ProcessID: 708 (0x2C4)
System Time is: 3/21/2000 4:3:0:264
Generating component: 8
Status: 14
Detection Location: 311
Flags:
Parameter 0:(Long value) : -30976 (0xFFFF8700)
Parameter 1:(Long value) : 16777343 (0x100007F)
```

 

 






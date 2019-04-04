---
title: rpcexts.eeinfo
description: Rpcexts.eeinfo 拡張機能では、拡張エラー情報のチェーンが表示されます。
ms.assetid: dc842236-bdbf-42aa-911d-6eb5eb1798ee
keywords:
- デバッグ rpcexts.eeinfo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.eeinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b407313efbc22b1c1cc60249a9856443679384f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579668"
---
# <a name="rpcextseeinfo"></a>!rpcexts.eeinfo


**! Rpcexts.eeinfo**拡張機能が拡張エラー情報のチェーンが表示されます。

```dbgcmd
!rpcexts.eeinfo EEInfoAddress
```

## <a name="span-idddkrpcextseeinfodbgspanspan-idddkrpcextseeinfodbgspanparameters"></a><span id="ddk__rpcexts_eeinfo_dbg"></span><span id="DDK__RPCEXTS_EEINFO_DBG"></span>パラメーター


<span id="_______EEInfoAddress______"></span><span id="_______eeinfoaddress______"></span><span id="_______EEINFOADDRESS______"></span> *EEInfoAddress*   
拡張エラー情報のアドレスを指定します。

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

この拡張機能には、拡張エラー情報のチェーン内のすべてのレコードの内容が表示されます。

レコードが最初のレコードを最新の順に表示されます。 レコードは、破線の線で区切られます。

(これには 1 レコードのみ) 例を次に示します。

```dbgcmd
0:001> !rpcexts.eeinfo 0xb015f0
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

1 つのレコードを使用して、チェーンが非常に長い場合[ **! rpcexts.eerecord** ](-rpcexts-eerecord.md)代わりにします。

 

 






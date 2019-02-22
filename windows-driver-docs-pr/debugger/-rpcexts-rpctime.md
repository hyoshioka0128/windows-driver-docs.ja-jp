---
title: rpcexts.rpctime
description: Rpcexts.rpctime 拡張機能では、現在のシステム時刻が表示されます。
ms.assetid: 72d54357-6b16-4d53-9909-ba201bb33519
keywords:
- デバッグ rpcexts.rpctime Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.rpctime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 645a9c477d60059a22228fdff7f153f0d9a14ae6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560578"
---
# <a name="rpcextsrpctime"></a>!rpcexts.rpctime


**! Rpcexts.rpctime**拡張機能には、現在のシステム時刻が表示されます。

```dbgcmd
!rpcexts.rpctime 
```

## <span id="ddk__rpcexts_rpctime_dbg"></span><span id="DDK__RPCEXTS_RPCTIME_DBG"></span>


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

 

<a name="remarks"></a>注釈
-------

この拡張機能は、CDB と WinDbg のユーザー モードにのみ使用できます。

以下に例を示します。

```dbgcmd
0:001> !rpcexts.rpctime
Current time is: 059931.126  (0x00ea1b.07e)
```

 

 






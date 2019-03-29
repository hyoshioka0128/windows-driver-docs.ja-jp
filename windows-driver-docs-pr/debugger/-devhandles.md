---
title: devhandles
description: Devhandles 拡張機能では、指定されたデバイス、開いているハンドルが表示されます。
ms.assetid: a473dd58-1571-4969-b8b7-f7a71128d824
keywords:
- Windows デバッグ devhandles
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devhandles
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3145c0e050e4bf8cfc090a856dd5b39489209d8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578943"
---
# <a name="devhandles"></a>!devhandles


**! Devhandles**拡張機能には、指定されたデバイス、開いているハンドルが表示されます。

```dbgcmd
!devhandles Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
開いているハンドルを表示するデバイスのアドレスを指定します。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

ハンドルの完全な情報を表示するには、この拡張機能には、プライベート シンボルが必要です。

デバイス オブジェクトのアドレスを使用して取得することができます、 [ **! drvobj** ](-drvobj.md)または[ **! devnode** ](-devnode.md)拡張機能。

切り捨てられた例を次に示します。

```dbgcmd
lkd> !devhandles 0x841153d8

Checking handle table for process 0x840d3940
Handle table at 95fea000 with 578 Entries in use

Checking handle table for process 0x86951d90
Handle table at 8a8ef000 with 28 Entries in use

...

Checking handle table for process 0x87e63650
Handle table at 947bc000 with 308 Entries in use

Checking handle table for process 0x87e6f4f0
00000000: Unable to read handle table
```

 

 






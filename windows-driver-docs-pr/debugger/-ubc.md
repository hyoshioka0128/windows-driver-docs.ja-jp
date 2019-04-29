---
title: ubc
description: Ubc 拡張機能は、ユーザー スペースのブレークポイントをクリアします。
ms.assetid: 4BF2C589-A1C4-4714-B712-DD52D04704D1
keywords:
- Windows デバッグ ubc
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa5cae2e4a05d2af80d6b88f7e4dca7841ea8bfd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334159"
---
# <a name="ubc"></a>!ubc


**! Ubc**拡張機能がユーザー スペースのブレークポイントをクリアします。

```dbgcmd
!ubc BreakpointNumber 
```

## <a name="span-idddkubcdbgspanspan-idddkubcdbgspanparameters"></a><span id="ddk__ubc_dbg"></span><span id="DDK__UBC_DBG"></span>パラメーター


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span> *BreakpointNumber*   
削除するブレークポイントの数を指定します。 アスタリスク (\*) すべてのブレークポイントを示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

これで設定されたブレークポイントを完全に削除されます[ **! ubp**](-ubp.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**! スキャナー**](-ubd.md)

[**! ube**](-ube.md)

[**!ubl**](-ubl.md)

[**! ubp**](-ubp.md)

[ユーザー領域とシステム領域](user-space-and-system-space.md)

 

 







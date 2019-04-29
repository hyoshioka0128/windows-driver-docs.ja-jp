---
title: ube
description: Ube 拡張機能をユーザー スペースのブレークポイントを再度有効にします。
ms.assetid: caa13c30-e03a-44fd-9221-66e44eec88af
keywords:
- Windows デバッグ ube
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ube
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1eb9555fb292fadc4aa65987aa70bf4a08f2b625
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334155"
---
# <a name="ube"></a>!ube


**! Ube**拡張機能ユーザー スペースのブレークポイントを再度有効にします。

```dbgcmd
!ube BreakpointNumber 
```

## <a name="span-idddkubedbgspanspan-idddkubedbgspanparameters"></a><span id="ddk__ube_dbg"></span><span id="DDK__UBE_DBG"></span>パラメーター


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span> *BreakpointNumber*   
有効にするブレークポイントの数を指定します。 アスタリスク (\*) すべてのブレークポイントを示します。

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

これには、使用して無効になっていたブレークポイントを再度有効にする[ **! スキャナー**](-ubd.md)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!ubc**](-ubc.md)

[**! スキャナー**](-ubd.md)

[**!ubl**](-ubl.md)

[**! ubp**](-ubp.md)

[ユーザー領域とシステム領域](user-space-and-system-space.md)

 

 







---
title: スキャナー
description: スキャナーの拡張機能には、ユーザー スペースのブレークポイントを一時的に無効にします。
ms.assetid: a639c5e0-111c-45c7-ac7d-6b7e70c1de4f
keywords:
- Windows のデバッグは
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25306c912cd649d88880bc7255cec219c90b4678
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573019"
---
# <a name="ubd"></a>!ubd


**! スキャナー**拡張機能をユーザー スペースのブレークポイントを一時的に無効にします。

```dbgcmd
!ubd BreakpointNumber 
```

## <a name="span-idddkubddbgspanspan-idddkubddbgspanparameters"></a><span id="ddk__ubd_dbg"></span><span id="DDK__UBD_DBG"></span>パラメーター


<span id="_______BreakpointNumber______"></span><span id="_______breakpointnumber______"></span><span id="_______BREAKPOINTNUMBER______"></span> *BreakpointNumber*   
無効にするブレークポイントの数を指定します。 アスタリスク (\*) すべてのブレークポイントを示します。

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

 

<a name="remarks"></a>コメント
-------

無効になっているブレークポイントは無視されます。 使用[ **! ube** ](-ube.md)ブレークポイントを再度有効にします。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!ubc**](-ubc.md)

[**! ube**](-ube.md)

[**!ubl**](-ubl.md)

[**! ubp**](-ubp.md)

[ユーザー領域とシステム領域](user-space-and-system-space.md)

 

 







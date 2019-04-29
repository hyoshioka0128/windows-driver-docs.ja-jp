---
title: blockeddrv
description: Blockeddrv 拡張機能では、ターゲット コンピューターでブロックされたドライバーの一覧が表示されます。
ms.assetid: 38331ff6-1957-4b28-90c0-10b2c77339fb
keywords:
- ブロックされたドライバー
- Windows デバッグ blockeddrv
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- blockeddrv
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 983ba99bba1c47e2e49cc1f3727cc155a2f5d138
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334685"
---
# <a name="blockeddrv"></a>!blockeddrv


**! Blockeddrv**拡張機能は、ターゲット コンピューターでブロックされたドライバーの一覧を表示します。

```dbgcmd
    !blockeddrv
```

## <span id="ddk__blockeddrv_dbg"></span><span id="DDK__BLOCKEDDRV_DBG"></span>


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

 

<a name="remarks"></a>注釈
-------

以下に例を示します。

```dbgcmd
kd> !blockeddrv
Driver:      Status    GUID
afd.sys      0:        {00000008-0206-0001-0000-000030C964E1}
agp440.sys   0:        {0000005C-175A-E12D-5000-010020885580}
atapi.sys    0:        {0000005C-B04A-E12E-5600-000020885580}
audstub.sys  0:        {0000005C-B04A-E12E-5600-000020885580}
Beep.SYS     0:        {0000005C-B04A-E12E-5600-000020885580}
Cdfs.SYS     0:        {00000008-0206-0001-0000-000008F036E1}
.....
```

 

 






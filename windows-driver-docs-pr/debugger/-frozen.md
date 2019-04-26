---
title: 固定されています。
description: 固定された拡張機能では、各プロセッサの状態が表示されます。
ms.assetid: aa2761b7-e7e1-435e-98d3-bfaac64925bf
keywords:
- プロセッサの状態
- 固定された Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- frozen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40987edacdd353979b69b7f56cb3d57784573d3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336654"
---
# <a name="frozen"></a>!frozen


**! 固定**拡張機能には、各プロセッサの状態が表示されます。

```dbgcmd
!frozen
```

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

この拡張機能からの出力の例を次に示します。

```dbgcmd
0: kd> !frozen
Processor states:
       0 : Current
       1 : Frozen
```

 

 






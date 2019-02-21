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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551577"
---
# <a name="frozen"></a>! 固定


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

 

 






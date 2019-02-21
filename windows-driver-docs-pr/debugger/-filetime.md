---
title: filetime
description: Filetime の拡張機能は、64 ビットの FILETIME 構造体を人間が判読できる時間に変換します。
ms.assetid: 26ee9219-ad37-4b0e-b204-5ed6d93355b0
keywords:
- FILETIME
- filetime は Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- filetime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d3bb5075a06875a4f18b04dd415fb25b5ea9bb4e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529817"
---
# <a name="filetime"></a>! filetime


**! Filetime**拡張機能は、人間が判読できる時間に 64 ビットの FILETIME 構造体を変換します。

```dbgcmd
!filetime Time
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Time______"></span><span id="_______time______"></span><span id="_______TIME______"></span> *時間*   
64 ビットの FILETIME 構造体を指定します。

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

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !filetime 1c4730984712348
 7/26/2004 04:10:18.712 (Pacific Standard Time)
```

 

 






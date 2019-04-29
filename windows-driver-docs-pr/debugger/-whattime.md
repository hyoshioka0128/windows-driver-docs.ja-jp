---
title: whattime
description: Whattime 拡張機能は、ティック カウントを標準時の値に変換します。
ms.assetid: c63e8bad-3a87-4209-b9f0-b6c433c294b2
keywords:
- ティック数 (tick count)
- Windows デバッグ whattime
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- whattime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca6f8eb2d6e84afefbc253cdf59d474b0feaf2c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327958"
---
# <a name="whattime"></a>!whattime


**! Whattime**拡張機能は、標準時の値にティック カウントを変換します。

```dbgcmd
!whattime Ticks
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Ticks______"></span><span id="_______ticks______"></span><span id="_______TICKS______"></span> *ティック*   
タイマー刻みの数。

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

として、出力が表示されます*HH:MM:SS.mmm*します。 以下に例を示します。

```dbgcmd
kd> !whattime 29857ae4
696613604 Ticks in Standard Time:  15:02:16.040s
```

 

 






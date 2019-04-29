---
title: whatperftime
description: Whatperftime 拡張機能は、高解像度のパフォーマンス カウンターの値を標準時の値に変換します。
ms.assetid: ff11a51f-4e25-4cf3-be19-d38361c441e9
keywords:
- パフォーマンス カウント
- Windows デバッグ whatperftime
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- whatperftime
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bee6ad77a46605e333075c1f43e7ea53648567b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327956"
---
# <a name="whatperftime"></a>!whatperftime


**! Whatperftime**拡張機能は、標準時の値に高解像度のパフォーマンス カウンターの値を変換します。

```dbgcmd
!whatperftime Count
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
パフォーマンス カウンターのクロック値。

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

使用することができます **! whatperftime**に呼び出すことによって取得される値を変換する**QueryPerformanceCounter**します。 パフォーマンス カウンターの時刻の値は、ソフトウェア トレースにも存在します。

として、出力が表示されます*HH:MM:SS.mmm*します。 以下に例を示します。

```dbgcmd
kd> !whatperftime 304589
3163529 Performance Counter in Standard Time: .004.313s
```

 

 






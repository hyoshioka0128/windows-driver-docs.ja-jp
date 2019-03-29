---
title: dpa
description: Dpa 拡張機能では、プールの割り当て情報を表示します。
ms.assetid: 1eb31741-bc50-4188-823d-b6324d2dfdf1
keywords:
- プールの割り当て
- Windows デバッグ dpa
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dpa
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe33605cd5d0e161f5c6cac46a8c3c982c5e6121
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582061"
---
# <a name="dpa"></a>!dpa


**! Dpa**拡張機能は、プールの割り当て情報を表示します。

```dbgcmd
!dpa Options 
!dpa -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
必要があります正確に次のオプションのいずれか。

<span id="-c"></span><span id="-C"></span>**-c**  
現在のプール割り当ての統計情報が表示されます。

<span id="-v"></span><span id="-V"></span>**-v**  
現在のすべてのプール割り当てを表示します。

<span id="-vs"></span><span id="-VS"></span>**-vs**  
スタック トレースが表示をによりします。

<span id="-f"></span><span id="-F"></span>**-f**  
プールの割り当ての失敗が表示されます。

<span id="-r"></span><span id="-R"></span>**-r**  
空きプールの割り当てを表示します。

<span id="-p_Ptr"></span><span id="-p_ptr"></span><span id="-P_PTR"></span>**-p** **** *Ptr*  
ポインターが含まれているすべてのプール割り当てを表示します。 *Ptr*します。

<span id="_______-_______"></span> **-?**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

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

この拡張機能を操作するために、Win32k.sys でプール インストルメンテーションを有効にする必要があります。

 

 






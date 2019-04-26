---
title: kuser
description: Kuser 拡張機能では、ユーザー モードの共有 ページ (KUSER_SHARED_DATA) が表示されます。
ms.assetid: 352a2f96-ff66-41be-94ee-045edbb1f81f
keywords:
- Windows デバッグ kuser
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- kuser
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: df0ce99c1d41011a468b0edf042aec272cf3ff63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336204"
---
# <a name="kuser"></a>!kuser


**! Kuser**拡張機能には、共有のユーザー モード ページが表示されます (KUSER\_SHARED\_データ)。

```dbgcmd
!kuser 
```

## <span id="ddk__kuser_dbg"></span><span id="DDK__KUSER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KUSER\_SHARED\_データ ページには、リソースと、現在ログオンしているユーザーに関するその他の情報が表示されます。

次に例を示します。 なお、この例では、両方、未加工の形式ではかっこ内にあるユーザーにわかりやすい形式で、チック カウントが表示されます。 わかりやすい表示は、Windows XP でのみ使用可能な以降です。

```dbgcmd
kd> !kuser
_KUSER_SHARED_DATA at 7ffe0000
TickCount:    fa00000 * 00482006 (0:20:30:56.093)
TimeZone Id: 2
ImageNumber Range: [14c .. 14c]
Crypto Exponent: 0
SystemRoot: 'F:\WINDOWS'
```

 

 






---
title: imgreloc
description: Imgreloc 拡張機能では、読み込まれている各モジュールのアドレスを表示しが再配置する前に、元のアドレスを示します。
ms.assetid: 79b729bd-7e4f-4167-b049-8a5c23cb8787
keywords:
- Windows デバッグ imgreloc
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- imgreloc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e3ab5678381a6cca0945f76a46dc13bc1c184445
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336425"
---
# <a name="imgreloc"></a>!imgreloc


**! Imgreloc**拡張機能が読み込まれている各モジュールのアドレスを表示してが再配置する前に、元のアドレスを示します。

```dbgcmd
!imgreloc Address 
```

## <a name="span-idddkimgrelocdbgspanspan-idddkimgrelocdbgspanparameters"></a><span id="ddk__imgreloc_dbg"></span><span id="DDK__IMGRELOC_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
イメージのベース アドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

以下に例を示します。

```dbgcmd
0:000> !imgreloc 00400000
00400000 Prymes - at preferred address
010e0000 appvcore - RELOCATED from 00400000
5b2f0000 verifier - at preferred address
5d160000 ShimEng - at preferred address
```

 

 






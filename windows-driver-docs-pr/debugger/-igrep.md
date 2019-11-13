---
title: igrep
description: igrep 拡張機能は、逆アセンブリ内のパターンを検索します。
ms.assetid: f76aa84b-6d52-4b36-b2d0-d4a8d47d510e
keywords:
- Windows デバッグ igrep
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- igrep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c3696a8748cb5b84de485d2ba700708454626b7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336449"
---
# <a name="igrep"></a>!igrep


**!igrep** 逆アセンブリ内のパターンの拡張機能を検索します。

```dbgcmd
!igrep [Pattern [StartAddress]] 
```

## <a name="span-idddk__igrep_dbgspanspan-idddk__igrep_dbgspanparameters"></a><span id="ddk__igrep_dbg"></span><span id="DDK__IGREP_DBG"></span>パラメーター


<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
検索するパターンを指定します。 省略すると、最後の*パターン*使用されます。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
検索を開始する位置の 16 進数のアドレスを指定します。 省略すると、現在のプログラム カウンターが使用されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

 

 






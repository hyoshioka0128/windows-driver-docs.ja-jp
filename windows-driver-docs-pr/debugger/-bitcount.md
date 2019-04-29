---
title: bitcount
description: '! Bitcount 拡張機能は、メモリの範囲内の「1」のビット数をカウントします。'
ms.assetid: dacf3d63-6241-4779-afca-514905b37e26
keywords:
- Windows デバッグ bitcount
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bitcount
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e5b05f50dd6941ae1fc1ffee34db45a4cdeb5789
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334695"
---
# <a name="bitcount"></a>!bitcount


**! Bitcount**拡張機能は、メモリの範囲内の「1」のビット数をカウントします。

```dbgcmd
!bitcount StartAddress TotalBits
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
カウントされる「1」のビットをメモリ範囲の開始アドレスを指定します。

<span id="_______TotalBits______"></span><span id="_______totalbits______"></span><span id="_______TOTALBITS______"></span> *TotalBits*   
メモリの範囲のサイズをビット単位で指定します。

<span id="_______-_______"></span> **-?**   
この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

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
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

 

 






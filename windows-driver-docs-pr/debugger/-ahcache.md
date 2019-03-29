---
title: ahcache
description: Ahcache 拡張機能は、アプリケーションの互換性のキャッシュを表示します。
ms.assetid: 65a7c320-3ea3-4657-b271-ec3d9c2bd5de
keywords:
- Windows デバッグ ahcache
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ahcache
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0bf1fed47df382824dded69c2aa6869f1d79cc16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572934"
---
# <a name="ahcache"></a>!ahcache


**! Ahcache**拡張機能は、アプリケーションの互換性のキャッシュを表示します。

```dbgcmd
!ahcache [Flags] 
```

## <a name="span-idddkahcachedbgspanspan-idddkahcachedbgspanparameters"></a><span id="ddk__ahcache_dbg"></span><span id="DDK__AHCACHE_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示に含める情報を指定します。 次のビット (既定値は 0) の任意の組み合わせこのことができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
RTL の表示\_ジェネリック\_LRU リストではなく、テーブルの一覧。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
詳細の表示: 名だけでなく、すべてのエントリ詳細が含まれています。

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

 

 

 






---
title: exchain
description: Exchain 拡張機能では、現在の例外ハンドラーのチェーンが表示されます。
ms.assetid: 6e5c935b-e475-4213-83d8-94510a58fde5
keywords:
- Windows デバッグ exchain
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- exchain
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1a820fcfb620faa1773f7aed5eddaf49da1b1aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334499"
---
# <a name="exchain"></a>!exchain


**! Exchain**拡張機能には、現在の例外ハンドラーのチェーンが表示されます。

```dbgcmd
!exchain [Options]
```

## <a name="span-idddkexchaindbgspanspan-idddkexchaindbgspanparameters"></a><span id="ddk__exchain_dbg"></span><span id="DDK__EXCHAIN_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のいずれかの値です。

<span id="_c"></span><span id="_C"></span>**/c**  
C のデバッグに関連する情報が表示されます**お試しください**/**キャッチ**このような例外が検出された場合は例外です。

<span id="_C"></span><span id="_c"></span>**/C**  
C のデバッグに関連する情報が表示されます**お試しください**/**キャッチ**例外、そのような例外が検出されない場合でもです。

<span id="_f"></span><span id="_F"></span>**/f**  
CRT の例外ハンドラーが検出されていない場合でも、CRT 関数のテーブルのウォークを取得する情報を表示します。

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

 

**! Exchain**拡張機能は、x86 ベースの移行先のコンピューターでのみ使用できます。

<a name="remarks"></a>注釈
-------

**! Exchain**拡張機能には、現在のスレッドの例外ハンドラーの一覧が表示されます。

リストがチェーン (例外を処理する最初のチャンスが指定されたもの) の最初のハンドラーで始まり末尾を継続します。 次の例では、この拡張機能を示します。

```dbgcmd
0:000> !exchain
0012fea8: Prymes!_except_handler3+0 (00407604)
  CRT scope  0, filter: Prymes!dzExcepError+e6 (00401576)
                func:   Prymes!dzExcepError+ec (0040157c)
0012ffb0: Prymes!_except_handler3+0 (00407604)
  CRT scope  0, filter: Prymes!mainCRTStartup+f8 (004021b8)
                func:   Prymes!mainCRTStartup+113 (004021d3)
0012ffe0: KERNEL32!GetThreadContext+1c (77ea1856)
```

 

 






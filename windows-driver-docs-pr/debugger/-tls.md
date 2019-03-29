---
title: tls
description: Tls 拡張機能は、スレッド ローカル ストレージ (TLS) スロットを表示します。
ms.assetid: 43325322-8e6e-47fc-b1ec-8b1c304bb1e9
keywords:
- TLS (スレッド ローカル ストレージ)
- スレッド ローカル ストレージ (TLS)
- Windows デバッグ tls
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tls
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bac89887b4586dcee99d1bec67589a58bec0c984
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572457"
---
# <a name="tls"></a>!tls


**! Tls**拡張機能は、スレッド ローカル ストレージ (TLS) スロットを表示します。

```dbgcmd
!tls Slot [TEB]
```

## <a name="span-idddktlsdbgspanspan-idddktlsdbgspanparameters"></a><span id="ddk__tls_dbg"></span><span id="DDK__TLS_DBG"></span>パラメーター


<span id="_______Slot______"></span><span id="_______slot______"></span><span id="_______SLOT______"></span> *スロット*   
TLS スロットを指定します。 0 ~ 1088 (10 進数) の間の任意の値を指定できます。 場合*スロット*-1 で、すべてのスロットが表示されます。

<span id="_______TEB______"></span><span id="_______teb______"></span> *TEB*   
スレッド環境ブロックの終了を指定します。 これは、0 または省略すると、現在のスレッドが使用されます。

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

 

<a name="remarks"></a>コメント
-------

以下に例を示します。

```dbgcmd
0:000> !tls -1
TLS slots on thread: c08.f54
0x0000 : 00000000
0x0001 : 003967b8
0:000> !tls 0
c08.f54: 00000000
```

 

 






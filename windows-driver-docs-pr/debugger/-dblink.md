---
title: dblink
description: Dblink 拡張機能は、後方リンクのリストを表示します。
ms.assetid: d57b07a6-217b-475e-adf5-7dc0f972c494
keywords:
- Windows デバッグ dblink
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dblink
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1461ca8b452874bde6841b7ba9a54e41f0fb2151
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528469"
---
# <a name="dblink"></a>!dblink


**! Dblink**拡張機能は、後方リンク リストを表示します。

```dbgcmd
!dblink Address [Count] [Bias]  
```

## <a name="span-idddkdblinkdbgspanspan-idddkdblinkdbgspanparameters"></a><span id="ddk__dblink_dbg"></span><span id="DDK__DBLINK_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
リストのアドレスを指定します\_エントリの構造体。 このノードに表示が開始されます。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
表示するリストのエントリの最大数を指定します。 これを省略すると、既定値は 32 です。

<span id="_______Bias______"></span><span id="_______bias______"></span><span id="_______BIAS______"></span> *バイアス*   
各ポインターで無視するビット マスクを指定します。 各**点滅**アドレスで and 演算は、(いない*バイアス*) 実行する前に、次の場所にします。 既定値は 0 (つまり、任意のビットは無視されません)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**! Dblink**拡張子横断、**点滅**リストのフィールド\_エントリの構造および各アドレスにある 4 つ ULONGs までが表示されます。 他の方向には、次のように使用します。 [ **! dflink**](-dflink.md)します。

[ **Dl (リンクされたリストを表示)** ](dl--display-linked-list-.md)コマンドより汎用性の高い **! dblink**と[ **! dflink**](-dflink.md)します。

 

 






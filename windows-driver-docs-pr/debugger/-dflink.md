---
title: dflink
description: Dflink 拡張機能では、順方向にリンクされたリストが表示されます。
ms.assetid: b75a01f6-557c-4602-83fa-629e16ba8c5d
keywords:
- Windows デバッグ dflink
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dflink
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74ebe7ae760ea6e1d35bddd08a80c5321dd2ebfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334589"
---
# <a name="dflink"></a>!dflink


**! Dflink**拡張機能では、順方向にリンクされた一覧が表示されます。

```dbgcmd
!dflink Address [Count] [Bias]  
```

## <a name="span-idddkdflinkdbgspanspan-idddkdflinkdbgspanparameters"></a><span id="ddk__dflink_dbg"></span><span id="DDK__DFLINK_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
リストのアドレスを指定します\_エントリの構造体。 このノードに表示が開始されます。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
表示するリストのエントリの最大数を指定します。 これを省略すると、既定値は 32 です。

<span id="_______Bias______"></span><span id="_______bias______"></span><span id="_______BIAS______"></span> *バイアス*   
各ポインターで無視するビット マスクを指定します。 各**Flink**アドレスで and 演算は、(いない*バイアス*) 実行する前に、次の場所にします。 既定値は 0 (つまり、任意のビットは無視されません)。

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

**! Dflink**拡張子横断、 **Flink**リストのフィールド\_エントリの構造および各アドレスにある 4 つ ULONGs までが表示されます。 他の方向には、次のように使用します。 [ **! dblink**](-dblink.md)します。

[ **Dl (リンクされたリストを表示)** ](dl--display-linked-list-.md)コマンドより汎用性の高い[ **! dblink** ](-dblink.md)と **! dflink**します。

 

 






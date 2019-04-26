---
title: gpiokd.pintable
description: Gpiokd.pintable コマンドでは、GPIO ピン配列に関する情報が表示されます。
ms.assetid: CBBC9BC7-D1BF-44C2-836B-703F5384D690
keywords:
- デバッグ gpiokd.pintable Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.pintable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97a7b399f83e38a338d98fbfefb6e1988cd68bb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336547"
---
# <a name="gpiokdpintable"></a>!gpiokd.pintable


**! Gpiokd.pintable**コマンドの GPIO ピン配列に関する情報を表示します。

```dbgcmd
!gpiokd.pintable PinBase PinCount [Flags]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______PinBase______"></span><span id="_______pinbase______"></span><span id="_______PINBASE______"></span> *PinBase*   
配列のアドレス[ \_GPIO\_PIN\_情報\_エントリ](gpio-extensions.md#data-structures-used-by-the-gpio-commands)構造体。

<span id="_______PinCount______"></span><span id="_______pincount______"></span><span id="_______PINCOUNT______"></span> *PinCount*   
表示されるピンの数。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
情報を指定するフラグが表示されます。 このパラメーターは、次のフラグの 1 つ以上のビットごとの OR です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="0x1"></span><span id="0X1"></span>0x1</p></td>
<td align="left"><p>このコマンドでは使用されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>このコマンドでは使用されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>表示には、未構成の pin が含まれています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[GPIO 拡張機能](gpio-extensions.md)

 

 







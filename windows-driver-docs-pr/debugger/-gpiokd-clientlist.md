---
title: gpiokd.clientlist
description: Gpiokd.clientlist コマンドでは、すべての登録済みの GPIO コント ローラーが表示されます。
ms.assetid: 4951C2D2-FA98-4600-A98D-1BC98080D2EB
keywords:
- デバッグ gpiokd.clientlist Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.clientlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1e94768331f8175c0a7cf425aa782d384e0d3e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553287"
---
# <a name="gpiokdclientlist"></a>!gpiokd.clientlist


**! Gpiokd.clientlist**コマンドは、すべての登録済みの GPIO コント ローラーを表示します。

```dbgcmd
!gpiokd.clientlist [Flags] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


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
<td align="left"><p>各コント ローラーに、その銀行のすべてを含む詳細な情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>ビット 0 (0x1) を設定し、このフラグ (0x2) が設定されて、各銀行のマスクの有効化とレジスタが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="0x4"></span><span id="0X4"></span>0x4</p></td>
<td align="left"><p>ビット 0 (0x1) が設定し、このフラグ (0x4) を設定、表示には、未構成の pin が含まれています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[GPIO 拡張機能](gpio-extensions.md)

 

 







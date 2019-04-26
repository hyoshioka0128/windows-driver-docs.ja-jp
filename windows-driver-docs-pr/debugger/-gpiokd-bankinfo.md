---
title: gpiokd.bankinfo
description: Gpiokd.bankinfo コマンドでは、GPIO 銀行に関する情報が表示されます。
ms.assetid: C4AFF469-0624-4D59-AE78-9D7FC407AC3A
keywords:
- デバッグ gpiokd.bankinfo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.bankinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b6f8f2ec0ac79179f8b44c926a8234dbaf50920
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336587"
---
# <a name="gpiokdbankinfo"></a>!gpiokd.bankinfo


**! Gpiokd.bankinfo**コマンドは、GPIO 銀行に関する情報を表示します。

```dbgcmd
!gpiokd.bankinfo BankAddress [Flags]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______BankAddress______"></span><span id="_______bankaddress______"></span><span id="_______BANKADDRESS______"></span> *BankAddress*   
アドレスを[ \_GPIO\_銀行\_エントリ](gpio-extensions.md#data-structures-used-by-the-gpio-commands)GPIO コント ローラーの銀行を表す構造体です。

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
<td align="left"><p>ピン留めするテーブルを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>有効にする] および [マスクのレジスタが表示されます。</p></td>
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

 

 







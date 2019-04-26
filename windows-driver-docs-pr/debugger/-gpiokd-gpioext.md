---
title: gpiokd.gpioext
description: Gpiokd.gpioext コマンドでは、GPIO コント ローラーに関する情報が表示されます。
ms.assetid: D5DB5166-A173-409E-A6A1-3872A22D19E1
keywords:
- デバッグ gpiokd.gpioext Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gpiokd.gpioext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd5d879945651d9bce11aa971c237211ff393594
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336565"
---
# <a name="gpiokdgpioext"></a>!gpiokd.gpioext


**! Gpiokd.gpioext**コマンドは、GPIO コント ローラーに関する情報を表示します。

```dbgcmd
!gpiokd.gpioext ExtensionAddress [Flags]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______ExtensionAddress______"></span><span id="_______extensionaddress______"></span><span id="_______EXTENSIONADDRESS______"></span> *ExtensionAddress*   
アドレス、 [\_デバイス\_拡張子](gpio-extensions.md#data-structures-used-by-the-gpio-commands)GPIO コント ローラーを表す構造体です。

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
<td align="left"><p>各銀行の暗証番号 (pin) のテーブルが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="0x2"></span><span id="0X2"></span>0x2</p></td>
<td align="left"><p>ビット 0 (0x1) が設定し、このフラグ (0x2) を設定、表示には有効にするが含まれていて、各銀行のマスクを登録します。</p></td>
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

 

 







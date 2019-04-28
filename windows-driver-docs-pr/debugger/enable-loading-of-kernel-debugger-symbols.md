---
title: Enable loading of kernel debugger symbols
description: Enable loading of kernel debugger symbols
ms.assetid: ce047073-9cfd-4ab2-bd58-48a2acc55351
keywords:
- カーネル デバッガーのシンボル (グローバル フラグ) の読み込みを有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a59ea4dd2c1d1540302da4af371594c6faeb709
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363540"
---
# <a name="enable-loading-of-kernel-debugger-symbols"></a>Enable loading of kernel debugger symbols


## <span id="ddk_enable_loading_of_kernel_debugger_symbols_dtools"></span><span id="DDK_ENABLE_LOADING_OF_KERNEL_DEBUGGER_SYMBOLS_DTOOLS"></span>


**カーネル デバッガーのシンボルの読み込みを有効にする**フラグは、次の時間の Windows を起動するカーネル メモリ領域にカーネルのシンボルを読み込みます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>ksl</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x40000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_ENABLE_KDEBUG_SYMBOL_LOAD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネル フラグ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

カーネルのシンボルは、カーネルのプロファイリングとデバッグ ツール、高度なカーネルによって使用されます。

 

 






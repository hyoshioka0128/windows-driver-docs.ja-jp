---
title: Disable stack extension
description: Disable stack extension
ms.assetid: e4c95103-4f98-4f79-a46c-c8040e39791b
keywords:
- スタックの拡張機能 (グローバル フラグ) を無効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 554fac533a332b92db0c2cb62816f05a151fe00c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363957"
---
# <a name="disable-stack-extension"></a>Disable stack extension


## <span id="ddk_disable_stack_extension_dtools"></span><span id="DDK_DISABLE_STACK_EXTENSION_DTOOLS"></span>


**スタックの拡張機能を無効にする**フラグは、初期コミットされたメモリ以外のプロセスのスレッドのスタックを拡張することから、カーネルを防ぎます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>dse</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x10000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_DISABLE_STACK_EXTENSION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

この機能は、メモリ不足の状態 (スタックの拡張機能が失敗します) をシミュレートし、メモリ不足にも適切に実行すると予想される戦略的なシステム プロセスのテストに使用されます。

 

 






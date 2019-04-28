---
title: Enable heap tail checking
description: Enable heap tail checking
ms.assetid: d71b4567-55e7-49e6-a791-a292ad477c10
keywords:
- ヒープの末尾 (グローバル フラグ) のチェックを有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2dc92c023e19e1a0a7109b242274faad9f62395
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363427"
---
# <a name="enable-heap-tail-checking"></a>Enable heap tail checking


## <span id="ddk_enable_heap_tail_checking_dtools"></span><span id="DDK_ENABLE_HEAP_TAIL_CHECKING_DTOOLS"></span>


**ヒープの末尾のチェックを有効に**ヒープが解放されるときにバッファー オーバーランをチェック フラグを設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>HTC</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAIL_CHECK</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

このフラグは、各割り当ての末尾に短いパターンを追加します。 Windows ヒープ マネージャーは、ブロックが解放され、ヒープ マネージャーが、デバッガーを中断、ブロックが変更された場合、パターンを検出します。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[ヒープの無料のチェックを有効に](enable-heap-free-checking.md)、[ヒープ パラメーター チェックを有効にします。](enable-heap-parameter-checking.md)

 

 






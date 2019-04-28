---
title: Enable heap validation on call
description: Enable heap validation on call
ms.assetid: 779871e0-f8b9-4eb5-9869-8df67586ffab
keywords:
- (グローバル フラグ) の呼び出しでヒープの検証を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52ef3612e2222a88ee5ac0939e06a287d7579879
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379145"
---
# <a name="enable-heap-validation-on-call"></a>Enable heap validation on call


## <span id="ddk_enable_heap_validation_on_call_dtools"></span><span id="DDK_ENABLE_HEAP_VALIDATION_ON_CALL_DTOOLS"></span>


**呼び出しでヒープの検証を有効にする**ヒープ関数が呼び出されるたびに、ヒープ全体を検証するフラグ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>hvc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x80</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_VALIDATE_ALL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

このフラグに関連付けられたオーバーヘッド高を避けるためには、使用、 **HeapValidate**ヒープが破棄されるときなど、重要な局面で特に、このフラグを設定する代わりに関数。 ただし、このフラグは、プール内のランダムな破損を検出するために便利です。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[ヒープ パラメーター チェックを有効にします。](enable-heap-parameter-checking.md)

 

 






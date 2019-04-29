---
title: Enable heap free checking
description: Enable heap free checking
ms.assetid: d97d6aac-608c-4c0a-8702-c078ed4820db
keywords:
- ヒープの空き (グローバル フラグ) のチェックを有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e269447c45690ec48c6c188136aa5d324dfe869e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330702"
---
# <a name="enable-heap-free-checking"></a>Enable heap free checking


## <span id="ddk_enable_heap_free_checking_dtools"></span><span id="DDK_ENABLE_HEAP_FREE_CHECKING_DTOOLS"></span>


**ヒープの無料のチェックを有効に**フラグが解放されるときに各ヒープの割り当てを検証します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>hfc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x20</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_FREE_CHECK</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[ヒープの末尾のチェックを有効に](enable-heap-tail-checking.md)、[ヒープ パラメーター チェックを有効にします。](enable-heap-parameter-checking.md)

 

 






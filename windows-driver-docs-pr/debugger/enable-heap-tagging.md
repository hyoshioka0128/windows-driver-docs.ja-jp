---
title: Enable heap tagging
description: Enable heap tagging
ms.assetid: be877811-075c-4019-81dd-73a134d5fb81
keywords:
- ヒープ (グローバル フラグ) をタグ付けを有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bcb37128088c2461d316de5d8cc5a8e91dfebf9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330643"
---
# <a name="enable-heap-tagging"></a>Enable heap tagging


## <span id="ddk_enable_heap_tagging_dtools"></span><span id="DDK_ENABLE_HEAP_TAGGING_DTOOLS"></span>


**ヒープがタグ付けを有効にする**フラグは、ヒープの割り当てに一意のタグを割り当てます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>加熱</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x800</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAGGING</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

使用して、タグを表示することができます、 [ **! ヒープ**](-heap.md)デバッガー拡張機能 -t パラメーターを使用します。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[DLL をヒープでタグ付けを有効にします。](enable-heap-tagging-by-dll.md)

 

 






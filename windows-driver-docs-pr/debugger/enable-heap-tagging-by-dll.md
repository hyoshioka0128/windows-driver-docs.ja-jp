---
title: Enable heap tagging by DLL
description: Enable heap tagging by DLL
ms.assetid: d8f8f6f6-7365-4208-834f-3f5ccacdb7b6
keywords:
- DLL (グローバル フラグ) をヒープでタグ付けを有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f53fa81c682e0bd6d549ab6bb712310aa0afc77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330794"
---
# <a name="enable-heap-tagging-by-dll"></a>Enable heap tagging by DLL


## <span id="ddk_enable_heap_tagging_by_dll_dtools"></span><span id="DDK_ENABLE_HEAP_TAGGING_BY_DLL_DTOOLS"></span>


**DLL をヒープでタグ付けを有効にする**フラグは、同じ DLL によって作成されたヒープの割り当てに一意のタグを割り当てます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>htd</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x8000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAG_BY_DLL</p></td>
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

[ヒープのタグ付けを有効にします。](enable-heap-tagging.md)

 

 






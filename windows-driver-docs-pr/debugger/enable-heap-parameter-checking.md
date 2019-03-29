---
title: Enable heap parameter checking
description: Enable heap parameter checking
ms.assetid: e9c7a2e3-8e43-45e3-948b-6154da1359e2
keywords:
- ヒープのパラメーター (グローバル フラグ) をチェックを有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98ca7e47611a8b1e47665684d2f3181de517f062
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578098"
---
# <a name="enable-heap-parameter-checking"></a>Enable heap parameter checking


## <span id="ddk_enable_heap_parameter_checking_dtools"></span><span id="DDK_ENABLE_HEAP_PARAMETER_CHECKING_DTOOLS"></span>


**ヒープ パラメーター チェックを有効に**ヒープ関数が呼び出されるたびに、ヒープの選択した要素の検証をフラグ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>hpc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x40</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_VALIDATE_PARAMETERS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[呼び出しでヒープの検証を有効にします。](enable-heap-validation-on-call.md)

 

 






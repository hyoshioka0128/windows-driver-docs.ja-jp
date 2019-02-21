---
title: カーネル スタックのページングを無効にします。
description: カーネル スタックのページングを無効にします。
ms.assetid: 3bf0ae20-4569-41de-9d7c-dd6a2790dac6
keywords:
- カーネル スタック (グローバル フラグ) のページングを無効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d02e9a57d9950e8012149d4c080f9ca175879735
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549746"
---
# <a name="disable-paging-of-kernel-stacks"></a>カーネル スタックのページングを無効にします。


## <span id="ddk_disable_paging_of_kernel_stacks_dtools"></span><span id="DDK_DISABLE_PAGING_OF_KERNEL_STACKS_DTOOLS"></span>


**カーネル スタックのページングを無効にする**フラグは、非アクティブなスレッドのカーネル モード スタックのページングを防止します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>dps</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>これに対して、0x80000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_DISABLE_PAGE_KERNEL_STACKS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

一般に、カーネル モード スタックはページングされたことはできません。メモリ内に存在するが保証されます。 ただし、Windows は、非アクティブなスレッドのカーネル スタックをページ場合があります。 このフラグは、これらの発生を防ぎます。

カーネル デバッガーは、そのスタックが物理メモリ内にある場合にのみ、スレッドに関する情報を提供できます。 このフラグは、特に重要なデッドロックをデバッグするときに、それ以外の場合は、すべてのスレッドを追跡する必要があります。

 

 






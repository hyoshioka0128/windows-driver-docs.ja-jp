---
title: Disable heap coalesce on free
description: Disable heap coalesce on free
ms.assetid: 64a68fa2-9270-4b2d-9edc-d54370191dcb
keywords:
- ヒープを無効にする無料 (グローバル フラグ) を結合
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef5b8fd7ff3da4569029b3cbcbd46474ce3a6666
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324605"
---
# <a name="disable-heap-coalesce-on-free"></a>Disable heap coalesce on free


## <span id="ddk_disable_heap_coalesce_on_free_dtools"></span><span id="DDK_DISABLE_HEAP_COALESCE_ON_FREE_DTOOLS"></span>


**ヒープを無効にするには、無料で coalesce**フラグのままヒープ メモリの隣接するブロック個別解放されるときにします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>dhc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x00200000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_DISABLE_COALESCING</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

既定では、Windows は、新しく解放隣接するブロックを (「結合」) を 1 つのブロックに結合します。 ブロックを組み合わせることは時間がかかりますが強制的に連続したメモリを見つけられないときに、追加のメモリを割り当てるヒープの断片化を削減します。

このフラグは、古いアプリケーションとの互換性を維持するために使用されます。

 

 






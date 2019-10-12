---
title: Enable page heap
description: Enable page heap
ms.assetid: b889b7b7-721c-4ecf-bf59-c1ccc0bc735d
keywords:
- ページヒープを有効にする (グローバルフラグ)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1ffe23db6ad6ab653ddab9a9d2b2c12e998dd18
ms.sourcegitcommit: 0610366df5de756bf8aa6bfc631eba5e3cd84578
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "63363550"
---
# <a name="enable-page-heap"></a>Enable page heap


## <span id="ddk_enable_page_heap_dtools"></span><span id="DDK_ENABLE_PAGE_HEAP_DTOOLS"></span>


**ページヒープの有効化**フラグは、ページヒープの検証を有効にします。これは、割り当て操作や解放操作などの動的ヒープメモリ操作を監視し、検証時にヒープエラーが検出されたときにデバッガーを中断させます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>hpa</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16進数値</strong></p></td>
<td align="left"><p>0x02000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_PAGE_ALLOCS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリエントリ、カーネルフラグ、イメージファイルのレジストリエントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

このオプションを使用すると、システムレジストリまたはカーネルフラグとして設定されている場合に、イメージファイルに対して設定された場合はページヒープの完全な検証が有効になり、標準のページヒープの検証も

-   *ページヒープの完全な検証*( **/i**の場合) では、各割り当ての最後に予約済みの仮想メモリのゾーンが配置されます。

-   *標準のページヒープ検証*( **/r**または **/k**の場合) は、割り当ての最後にランダムなパターンを配置し、ヒープブロックが解放されたときのパターンを調べます。

イメージファイルに対してこのフラグを設定することは、コマンドラインでのイメージファイルに対して「 **gflags/p/enable**ファイルタイプ」を**入力すること**と同じです。

 

 






---
title: Enable page heap
description: Enable page heap
ms.assetid: b889b7b7-721c-4ecf-bf59-c1ccc0bc735d
keywords:
- ページ ヒープ (グローバル フラグ) を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1ffe23db6ad6ab653ddab9a9d2b2c12e998dd18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363550"
---
# <a name="enable-page-heap"></a>Enable page heap


## <span id="ddk_enable_page_heap_dtools"></span><span id="DDK_ENABLE_PAGE_HEAP_DTOOLS"></span>


**ページ ヒープを有効にする**を動的ヒープ メモリの割り当てや無料の操作などの操作を監視し、ベリファイア ヒープ エラーが検出したときにデバッガー中断が発生するページ ヒープの検証、フラグがオンにします。

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
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x02000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_HEAP_PAGE_ALLOCS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

このオプションは、完全ページ ヒープの検証にイメージ ファイルを設定する場合と、システム レジストリまたはカーネル フラグとして設定すると標準的なページ ヒープ検証できます。

-   *完全なヒープのページ検証*(の **/i**) 各割り当ての最後に予約済みの仮想メモリのゾーンに配置します。

-   *標準的なページ ヒープの検証*(の **/r**または **/k**) 割り当ての最後にランダムなパターンを配置し、ヒープ ブロックを解放するときに、パターンをチェックします。

イメージ ファイルは入力すると同じです。 このフラグを設定**gflags/p/enable** *ImageFile* **フル/** コマンドラインでイメージ ファイル。

 

 






---
title: 可能であれば大きなページを使用してイメージを読み込む
description: 可能であれば大きなページを使用してイメージを読み込む
ms.assetid: 7f75b5bd-cc25-4f09-9d60-55b86969d16b
keywords:
- 可能であれば大きなページを使用して (グローバル フラグ) のイメージを読み込み
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bccbe3e8f6ac111c0e2a0309391fe604f0391fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537027"
---
# <a name="load-image-using-large-pages-if-possible"></a>可能であれば大きなページを使用してイメージを読み込む


## <span id="ddk_load_image_using_large_pages_if_possible_dtools"></span><span id="DDK_LOAD_IMAGE_USING_LARGE_PAGES_IF_POSSIBLE_DTOOLS"></span>


**可能であれば大きなページを使用してイメージを読み込み**プロセス アドレス空間にバイナリをマップする場合 (4 KB) の標準の小さなページではなくように指示大きなページ (4 MB) を使用するシステムを設定します。

この設定は、物理メモリ内のページ テーブル エントリの数を大幅に減るため、大きな実行可能ファイルに最も役立ちます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>lpg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>(なし)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

この設定は、GlobalFlag レジストリ エントリの値としてではなく、個別のレジストリ エントリでその値が格納されているために、グローバル フラグでは技術的ではありません。 その結果、16 進数の値を使用して設定することはできませんし、イメージ ファイルをこの設定を選択するときに表示されます、**他の設定**表示のフィールド。

 

 






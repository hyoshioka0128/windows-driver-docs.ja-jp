---
title: watermarkPath XML 要素
description: watermarkPath XML 要素
ms.assetid: 3c64738b-4ead-4e78-a1bd-45d098a11dad
keywords:
- watermarkPath XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- watermarkPath XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 02359f3886acbad1a5c846c85ea9194fd6b81e4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548704"
---
# <a name="watermarkpath-xml-element"></a>watermarkPath XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**WatermarkPath**要素 DPInst は DPInst へようこそ ページと DPInst 完了 ページの左側に表示されるカスタムのウォーターマーク ビットマップのソース ファイルを指定します。

### <a name="element-tag"></a>要素タグ

```cpp
<watermarkPath>
```

### <a name="xml-attributes"></a>XML 属性

なし

### <a name="element-information"></a>要素情報

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>親要素</strong></p></td>
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong> </a>または<a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>言語</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>[ようこそ] ページと [終了] ページの左側にあるその DPInst ウォーターマーク ビットマップを含むファイルの名前を指定する文字列を表示します。 ウォーターマーク ファイルは、DPInst の実行可能ファイルを含むディレクトリである DPInst のルート ディレクトリに配置する必要があります (<em>DPInst.exe</em>)、または DPInst のルート ディレクトリ下のサブディレクトリ。 透かしビットマップ ファイルがサブディレクトリ内にある場合は、DPInst のルート ディレクトリに対して相対的な完全修飾ファイル名を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

A **watermarkPath**要素は、カスタマイズしますが、ローカライズされていないの子要素である場合、 **dpinst**要素。 A **watermarkPath**要素をカスタマイズおよびローカライズの子要素である場合、**言語**要素。

次のコード例に示します、 **watermarkPath**要素を指定する*データ\\Watermark.bmp*の左側にある DPInst を表示するウォーターマーク ビットマップのソースとして、開始して、ページを終了します。 カスタムの透かしビットマップ ファイルを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <watermarkPath>Data\Watermark.bmp</watermarkPath>
  ...
</dpinst>
```

場合、 **watermarkPath**要素が指定されていない、DPInst は既定の基準値を使用します。

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

[**言語**](language-xml-element.md)

 

 







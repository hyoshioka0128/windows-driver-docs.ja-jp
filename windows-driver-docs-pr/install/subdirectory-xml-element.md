---
title: subDirectory XML 要素
description: subDirectory XML 要素
ms.assetid: 41f86668-148e-4d7c-89b8-e3c21efffd7b
keywords:
- サブディレクトリの XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- subDirectory XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 00a729317a484965cdc19926b2e61aa62a49b841
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385879"
---
# <a name="subdirectory-xml-element"></a>subDirectory XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**サブディレクトリ**XML 要素を DPInst の作業ディレクトリの下で、1 つまたはすべてのサブディレクトリを指定します。

### <a name="element-tag"></a>要素タグ

```cpp
<subDirectory>
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
<td align="left"><p><a href="search-xml-element.md" data-raw-source="[&lt;strong&gt;search&lt;/strong&gt;](search-xml-element.md)"><strong>search</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>1 つまたはすべての DPInst 作業ディレクトリを基準にあるサブディレクトリを指定します。 この要素を含めることができます。</p>
<ul>
<li><p>特定のサブディレクトリを指定する文字列</p></li>
<li><p>ワイルドカード文字 (<strong>*</strong>) のすべてのサブディレクトリを指定するには</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、**検索**要素を 1 つ含む**サブディレクトリ**要素を指定する、 *i386* DPInst 作業の下のサブディレクトリディレクトリ。 カスタムのサブディレクトリを示すテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <search>
    <subDirectory>i386</subDirectory>
  </search>
  ...
</dpinst>
```

次のコード例に示します、**検索**要素を含む、**サブディレクトリ**DPInst の作業ディレクトリのサブディレクトリのすべてを指定する要素。 ワイルドカード文字 (\*) 太字のフォント スタイルに示したすべてのサブディレクトリを指定します。

```cpp
<search>
  <subDirectory>*</subDirectory>
</search>
```

## <a name="see-also"></a>関連項目


[**search**](search-xml-element.md)

 

 







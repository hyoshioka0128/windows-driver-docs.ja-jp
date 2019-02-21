---
title: サブディレクトリの XML 要素
description: サブディレクトリの XML 要素
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
ms.openlocfilehash: 634a7241ce4a3a6095c03df7c9d29fc0a4ec2f63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529027"
---
# <a name="subdirectory-xml-element"></a>サブディレクトリの XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

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

 

 







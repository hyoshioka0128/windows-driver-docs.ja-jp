---
title: XML 要素を検索します。
description: XML 要素を検索します。
ms.assetid: 34eff240-a96a-4b73-a001-5ea698e9f7ae
keywords:
- XML 要素のデバイスとドライバーのインストールを検索します。
topic_type:
- apiref
api_name:
- search XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 397fba7639374dcad7a28f22a44528674db45c62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530507"
---
# <a name="search-xml-element"></a>XML 要素を検索します。


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**検索**XML 要素 DPInst サブディレクトリを検索する INF ファイルに対して再帰的に指定された DPInst の作業ディレクトリの下に指示します。 1 つまたは複数のサブディレクトリが指定されて[**サブディレクトリの子要素**](subdirectory-xml-element.md)します。

### <a name="element-tag"></a>要素タグ

```cpp
<search>
```

### <a name="xml-attributes"></a>XML 属性

なし

### <a name="element-information"></a>**要素情報**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>親要素</strong></p></td>
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p><a href="subdirectory-xml-element.md" data-raw-source="[&lt;strong&gt;subDirectory&lt;/strong&gt;](subdirectory-xml-element.md)"><strong>サブディレクトリ</strong></a> (0 個以上)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、**検索**要素を 1 つ含む**サブディレクトリ**を指定する XML 要素、 *i386*サブディレクトリ。 DPInst は再帰的に検索[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)で、 *i386* DPInst の作業ディレクトリのサブディレクトリ。 カスタムのサブディレクトリを示すテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <search>
    <subDirectory>i386</subDirectory>
  </search>
  ...
</dpinst>
```

**注**  重複する子要素が許可されないため、各**サブディレクトリ**の子要素を**検索**要素は一意である必要があります。

 

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

[**subDirectory**](subdirectory-xml-element.md)

 

 







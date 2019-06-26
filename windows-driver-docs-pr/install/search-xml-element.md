---
title: search XML 要素
description: search XML 要素
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
ms.openlocfilehash: 341faceba86aeea5b85aadf63447d2205aaf7653
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374214"
---
# <a name="search-xml-element"></a>search XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

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

次のコード例に示します、**検索**要素を 1 つ含む**サブディレクトリ**を指定する XML 要素、 *i386*サブディレクトリ。 DPInst は再帰的に検索[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)で、 *i386* DPInst の作業ディレクトリのサブディレクトリ。 カスタムのサブディレクトリを示すテキストが太字のフォント スタイルで表示されます。

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

 

 







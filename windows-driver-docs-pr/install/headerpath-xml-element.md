---
title: headerPath XML 要素
description: headerPath XML 要素
ms.assetid: 9764fed5-75bc-4679-bae0-5bfe738268e2
keywords:
- headerPath XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- headerPath XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3a9b0a869b6993cae7d9494e7f542244f138abe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386413"
---
# <a name="headerpath-xml-element"></a>headerPath XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**HeaderPath** XML 要素を DPInst は DPInst EULA ページと DPInst のインストール ページの右上隅に表示されるカスタム ヘッダー ビットマップのソース ファイル名を指定します。

### <a name="element-tag"></a>要素タグ

```cpp
<headerPath>
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
<td align="left"><p>DPInst は DPInst 使用許諾契約書とインストールのページの右上隅に表示されるヘッダー ビットマップのファイル名を指定する文字列。 ヘッダーのビットマップ ファイルは、DPInst の実行可能ファイルを含むディレクトリである DPInst のルート ディレクトリに配置する必要があります (<em>DPInst.exe</em>)、または DPInst のルート ディレクトリ下のサブディレクトリ。 ヘッダーのビットマップ ファイルがサブディレクトリ内にある場合は、DPInst のルート ディレクトリに対して相対的な完全修飾ファイル名を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

A **headerPath**要素は、カスタマイズしますが、ローカライズされていないの子要素である場合、 **dpinst** XML 要素。 A **headerPath**要素をカスタマイズおよびローカライズの子要素である場合、**言語**XML 要素。

次のコード例に示します、 **headerPath**要素を指定する*データ\\Header.bmp* DPInst が DPInst EULA の右上隅に表示されるヘッダー ビットマップ ファイルとしてインストール ページと、インストール ページ。 カスタム ヘッダーのビットマップ ファイルを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <headerPath>Data\Header.bmp</headerPath>
  ...
</dpinst>
```

場合、 **headerPath**要素が指定されていない、DPInst は既定のヘッダー ビットマップを使用します。

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

[**言語**](language-xml-element.md)

 

 







---
title: icon XML 要素
description: icon XML 要素
ms.assetid: 1d5acaf7-ef90-40f7-a2f9-f1002207f3fb
keywords:
- アイコンの XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- icon XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 21ea8c4f5714d95833c43ed65bea650063c1dc1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579935"
---
# <a name="icon-xml-element"></a>icon XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**アイコン**XML 要素を DPInst は DPInst EULA ページに表示されるカスタム アイコンのソース ファイルを指定します。 DPInst では、このアイコンを使用して、Microsoft Windows タスク バー、デスクトップで DPInst を表します。 DPInst を表すエントリにも使用するアイコンを[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)、DPInst に追加する**プログラムと機能**コントロール パネルの 

**注**  DPInst は Windows Vista では、前にするドライバー パッケージのエントリを追加**プログラム追加と削除**コントロール パネルの します。

 

### <a name="element-tag"></a>要素タグ

```cpp
<icon>
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
<td align="left"><p>DPInst は DPInst EULA ページに表示されるアイコンを含むソース ファイルを指定する文字列。 アイコン ファイルは、DPInst の実行可能ファイルを含むディレクトリである DPInst のルート ディレクトリに配置する必要があります (<em>DPInst.exe</em>)、または DPInst のルート ディレクトリ下のサブディレクトリ。 アイコン ファイルがサブディレクトリ内にある場合は、DPInst のルート ディレクトリに対して相対的な完全修飾ファイル名を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

**アイコン**要素は、カスタマイズしますが、ローカライズされていないの子要素である場合、 **dpinst** XML 要素。 **アイコン**要素をカスタマイズおよびローカライズの子要素である場合、**言語**XML 要素。

次のコード例に示します、**アイコン**データを指定する要素\\Small.ico DPInst DPInst EULA ページに表示されるカスタム アイコンのソースとして。 カスタム アイコン ファイルを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <icon>Data\Eula.ico</icon>
  ...
</dpinst>
```

場合、**アイコン**要素が指定されていない、DPInst が既定のアイコンが表示されます。 このアイコンの位置は変更できません。

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

[**言語**](language-xml-element.md)

 

 







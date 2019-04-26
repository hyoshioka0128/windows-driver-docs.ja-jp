---
title: language XML 要素
description: language XML 要素
ms.assetid: 1fc6a3b4-379e-4fd3-b526-c4193e9e84c5
keywords:
- 言語の XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- language XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b2c28fc664e93ae4f4218153477459d5daffd56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356946"
---
# <a name="language-xml-element"></a>language XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**言語**XML 要素をローカライズし、DPInst は、そのウィザードのページに表示される項目をカスタマイズします。

### <a name="element-tag"></a>要素タグ

```cpp
<language>
```

### <a name="xml-attributes"></a>XML 属性

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>コード</strong></p></td>
<td align="left"><p>16 進数形式または 10 進形式の言語識別子です。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left"><p><a href="dpinsttitle-xml-element.md" data-raw-source="[&lt;strong&gt;dpinstTitle&lt;/strong&gt;](dpinsttitle-xml-element.md)"><strong>dpinstTitle</strong> </a> (0 個または 1)</p>
<p><a href="eula-xml-element.md" data-raw-source="[&lt;strong&gt;eula&lt;/strong&gt;](eula-xml-element.md)"><strong>使用許諾契約書</strong></a> (0 個または 1)</p>
<p><a href="eulaheadertitle-xml-element.md" data-raw-source="[&lt;strong&gt;eulaHeaderTitle&lt;/strong&gt;](eulaheadertitle-xml-element.md)"><strong>eulaHeaderTitle</strong> </a> (0 個または 1)</p>
<p><a href="eulanobutton-xml-element.md" data-raw-source="[&lt;strong&gt;eulaNoButton&lt;/strong&gt;](eulanobutton-xml-element.md)"><strong>eulaNoButton</strong> </a> (0 個または 1)</p>
<p><a href="eulayesbutton-xml-element.md" data-raw-source="[&lt;strong&gt;eulaYesButton&lt;/strong&gt;](eulayesbutton-xml-element.md)"><strong>eulaYesButton</strong> </a> (0 個または 1)</p>
<p><a href="finishtext-xml-element.md" data-raw-source="[&lt;strong&gt;finishText&lt;/strong&gt;](finishtext-xml-element.md)"><strong>finishText</strong> </a> (0 個または 1)</p>
<p><a href="finishtitle-xml-element.md" data-raw-source="[&lt;strong&gt;finishTitle&lt;/strong&gt;](finishtitle-xml-element.md)"><strong>finishTitle</strong> </a> (0 個または 1)</p>
<p><a href="headerpath-xml-element.md" data-raw-source="[&lt;strong&gt;headerPath&lt;/strong&gt;](headerpath-xml-element.md)"><strong>headerPath</strong> </a> (0 個または 1)</p>
<p><a href="icon-xml-element.md" data-raw-source="[&lt;strong&gt;icon&lt;/strong&gt;](icon-xml-element.md)"><strong>アイコン</strong></a> (0 個または 1)</p>
<p><a href="installheadertitle-xml-element.md" data-raw-source="[&lt;strong&gt;installHeaderTitle&lt;/strong&gt;](installheadertitle-xml-element.md)"><strong>installHeaderTitle</strong> </a> (0 個または 1)</p>
<p><a href="watermarkpath-xml-element.md" data-raw-source="[&lt;strong&gt;watermarkPath&lt;/strong&gt;](watermarkpath-xml-element.md)"><strong>watermarkPath</strong> </a> (0 個または 1)</p>
<p><a href="welcomeintro-xml-element.md" data-raw-source="[&lt;strong&gt;welcomeIntro&lt;/strong&gt;](welcomeintro-xml-element.md)"><strong>welcomeIntro</strong> </a> (0 個または 1)</p>
<p><a href="welcometitle-xml-element.md" data-raw-source="[&lt;strong&gt;welcomeTitle&lt;/strong&gt;](welcometitle-xml-element.md)"><strong>welcomeTitle</strong> </a> (0 個または 1)</p></td>
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

使用することができます、**言語**ローカライズし、テキスト、アイコン、および DPInst は、そのウィザードのページに表示されるビットマップをカスタマイズする要素。 アイコンは、Microsoft Windows タスク バーと Windows デスクトップ DPInst を表します。

DPInst に追加されるエントリにも使用するアイコン**プログラムと機能**コントロール パネルの します。 これらのエントリを表す、[ドライバー パッケージ](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)DPInst をインストールします。

**注**  DPInst がそれらのエントリを追加する Windows Vista より前のバージョンの Windows で**プログラム追加と削除**コントロール パネルの します。

 

DPInst の英語専用バージョンのウィザード ページに表示される項目をカスタマイズする、**言語**要素を英語 (標準) 言語を指定しの子要素を含める、**言語**項目をカスタマイズする要素。 ローカライズと多言語版 DPInst DPInst ウィザード ページに表示される項目をカスタマイズを使用して、**言語**要素の子要素を含める言語を指定する、**言語**項目をカスタマイズする要素。

次のコード例に示します、**言語**英語 (Standard) の言語を指定し含む、要素をカスタマイズ**dpinstTitle**と**welcomeTitle**XML 子要素。 カスタムのテキストを指定するテキストが太字のフォントの種類で表示されます。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <dpinstTitle>Toaster Device Installer</dpinstTitle>
    <welcomeTitle>Welcome to the toaster Installer!</welcomeTitle>
    ...
  </language>
  ...
</dpinst>
```

場合、 **dpinstTitle**要素が指定されていない、DPInst は、既定の [ようこそ] ページに表示される既定のタイトル バーのテキストを表示します。

## <a name="see-also"></a>関連項目


[**dpinstTitle**](dpinsttitle-xml-element.md)

[**使用許諾契約書**](eula-xml-element.md)

[**eulaHeaderTitle**](eulaheadertitle-xml-element.md)

[**eulaNoButton**](eulanobutton-xml-element.md)

[**eulaYesButton**](eulayesbutton-xml-element.md)

[**finishText**](finishtext-xml-element.md)

[**finishTitle**](finishtitle-xml-element.md)

[**headerPath**](headerpath-xml-element.md)

[**icon**](icon-xml-element.md)

[**installHeaderTitle**](installheadertitle-xml-element.md)

[**watermarkPath**](watermarkpath-xml-element.md)

[**welcomeIntro**](welcomeintro-xml-element.md)

[**welcomeTitle**](welcometitle-xml-element.md)

 

 







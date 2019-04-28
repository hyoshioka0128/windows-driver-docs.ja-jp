---
title: eulaYesButton XML 要素
description: eulaYesButton XML 要素
ms.assetid: 7d91d3ec-af0a-4b6a-83d8-fa14a527378b
keywords:
- eulaYesButton XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- eulaYesButton XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a275f253e87da2085fc1557ef5f5964d4dcc19b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360620"
---
# <a name="eulayesbutton-xml-element"></a>eulaYesButton XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**EulaYesButton** DPInst EULA ページの承認のオプション ボタンに関連付けられているテキストをカスタマイズする XML 要素。

### <a name="element-tag"></a>**要素タグ**

```cpp
<eulaYesButton>
```

### <a name="xml-attributes"></a>**XML 属性**

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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>言語</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>DPInst EULA ページの承認のオプション ボタンに関連付けられているテキストをカスタマイズする文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **eulaYesButton** DPInst 使用許諾契約書 ページで同意オプション ボタンのテキストをカスタマイズする要素。 カスタム承認のオプション ボタンのテキストを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <eulaYesButton>I &amp;accept this EULA</eulaYesButton>
    ...
  </language>
  ...
</dpinst>
```

場合、 **eulaYesButton**要素が指定されていない、DPInst 既定 DPInst 使用許諾契約書 ページに表示される既定のオプション ボタンのテキストを表示します。

## <a name="see-also"></a>関連項目


[**使用許諾契約書**](eula-xml-element.md)

[**eulaNoButton**](eulanobutton-xml-element.md)

[**言語**](language-xml-element.md)

 

 







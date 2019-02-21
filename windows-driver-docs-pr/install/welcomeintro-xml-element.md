---
title: welcomeIntro XML 要素
description: welcomeIntro XML 要素
ms.assetid: d0325d14-c31a-453d-b28e-4bdb646d0711
keywords:
- welcomeIntro XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- welcomeIntro XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e93f6cbe0071a1a68fbd3791fb88ca71e2ad5011
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538444"
---
# <a name="welcomeintro-xml-element"></a>welcomeIntro XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**WelcomeIntro** XML 要素が DPInst へようこそ ページでメイン テキストをカスタマイズします。

### <a name="element-tag"></a>要素タグ

```cpp
<welcomeIntro>
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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>言語</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>[ようこそ] ページのメイン テキストをカスタマイズする文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **welcomeIntro**へようこそ ページでメイン テキストをカスタマイズする要素。 カスタムの [ようこそ] の概要を示すテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    . . .
    <welcomeIntro>This wizard will walk you through updating the drivers for your Toaster device.</welcomeIntro>
    ...
  </language>
  ...
</dpinst>
```

場合、 **welcomeIntro**要素が指定されていない、DPInst は既定の [ようこそ] ページに表示される既定のメイン テキストを表示します。

## <a name="see-also"></a>関連項目


[**言語**](language-xml-element.md)

 

 







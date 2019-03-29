---
title: welcomeTitle XML 要素
description: welcomeTitle XML 要素
ms.assetid: 480b6d02-b8b1-4e3f-9a00-869cc2b93279
keywords:
- welcomeTitle XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- welcomeTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b67cb60d4271241bce77bc60ced1caa50315d56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580869"
---
# <a name="welcometitle-xml-element"></a>welcomeTitle XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**WelcomeTitle** XML 要素が DPInst へようこそ ページの上部に表示される ようこそ のタイトルの太字のテキストをカスタマイズします。

### <a name="element-tag"></a>要素タグ

```cpp
<welcomeTitle>
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
<td align="left"><p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>言語</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>[ようこそ] ページの上部でタイトルのテキストをカスタマイズする文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **welcomeTitle**要素は、[ようこそ] ページのタイトル テキストをカスタマイズします。 カスタムの [ようこそ] のタイトルを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <welcomeTitle>Welcome to the toaster Installer!</welcomeTitle>
    ...
  </language>
  ...
</dpinst>
```

場合、 **welcomeTitle**要素が指定されていない、DPInst は既定の [ようこそ] ページに表示される既定のようこそタイトルを表示します。

## <a name="see-also"></a>関連項目


[**言語**](language-xml-element.md)

 

 







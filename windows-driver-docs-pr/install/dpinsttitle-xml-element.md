---
title: dpinstTitle XML 要素
description: dpinstTitle XML 要素
ms.assetid: a6867874-436b-414f-9610-aea585822a91
keywords:
- dpinstTitle XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- dpinstTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b13908ba80e41fb9c5a1b7b0431c147e13a0aa32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375286"
---
# <a name="dpinsttitle-xml-element"></a>dpinstTitle XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**DpinstTitle** XML 要素は、すべての DPInst ウィザード ページのタイトル バーに表示されるテキストをカスタマイズします。

### <a name="element-tag"></a>要素タグ

```cpp
<dpinstTitle>
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
<td align="left"><p>文字列のすべてのウィザード ページのタイトル バーのテキストをカスタマイズします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例、 **dpinstTitle**要素は、タイトル バーのテキストをカスタマイズします。 カスタムの DPInst タイトルを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    ...
    <dpinstTitle>Toaster Device Installer</dpinstTitle>
    ...
  </language>
  ...
</dpinst>
```

場合、 **dpinstTitle**要素が指定されていない、DPInst は、既定の [ようこそ] ページに表示される既定のタイトル バーのテキストを表示します。

## <a name="see-also"></a>関連項目


[**言語**](language-xml-element.md)

 

 







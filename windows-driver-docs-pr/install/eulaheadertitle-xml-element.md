---
title: eulaHeaderTitle XML 要素
description: eulaHeaderTitle XML 要素
ms.assetid: 65b8e793-ed7b-4d2c-8a55-9860e6188b77
keywords:
- eulaHeaderTitle XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- eulaHeaderTitle XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7d1430e16364f9ca912759a86e39524652e42166
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364106"
---
# <a name="eulaheadertitle-xml-element"></a>eulaHeaderTitle XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**EulaHeaderTitle** XML 要素が DPInst EULA ページのタイトル バーを下に表示される使用許諾契約書ヘッダー タイトルのテキストをカスタマイズします。

### <a name="element-tag"></a>要素タグ

```cpp
<eulaHeaderTitle>
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
<td align="left"><p>DPInst EULA ページのタイトルをカスタマイズする文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

次のコード例に示します、 **eulaHeaderTitle** DPInst EULA ページのヘッダーのタイトルをカスタマイズする要素。 カスタム ヘッダーのタイトルを指定するテキストが太字のフォント スタイルで表示されます。

```cpp
<dpinst>
  ...
  <language code="0x0409">
    . . .
    <eulaHeaderTitle>End User License Agreement</eulaHeaderTitle>
    . . .
  </language>
  ...
</dpinst>
```

場合、 **eulaHeaderTitle**要素が指定されていない、DPInst 既定既定 DPInst 使用許諾契約書 ページに表示される使用許諾契約書ヘッダー タイトルを表示します。

## <a name="see-also"></a>関連項目


[**言語**](language-xml-element.md)

 

 







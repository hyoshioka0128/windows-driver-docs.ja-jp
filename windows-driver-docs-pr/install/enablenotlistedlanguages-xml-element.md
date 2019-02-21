---
title: enableNotListedLanguages XML 要素
description: EnableNotListedLanguages XML 要素は、空の要素には、構成のサポートされている言語が明示的に有効でない DPInst.xml ファイルの言語の XML 要素をすべて有効にする DPInst enableNotListedLanguages フラグを設定します。
ms.assetid: 7584b222-71b0-4532-84be-3444a4a7003b
keywords:
- enableNotListedLanguages XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- enableNotListedLanguages XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9aeed2c3718fc679de8b72f52ce705a1dc914779
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536532"
---
# <a name="enablenotlistedlanguages-xml-element"></a>enableNotListedLanguages XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**EnableNotListedLanguages** XML 要素が空の要素を設定する、 **enableNotListedLanguages** DPInst はサポートされている言語のすべてを有効にするを構成するには、フラグ明示的に有効になって[**言語**](language-xml-element.md)内の XML 要素を*DPInst.xml*ファイル。

### <a name="element-tag"></a>要素タグ

```cpp
<enableNotListedLanguages>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
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

既定では、DPInst でサポートされている言語のすべてが有効になっている場合、 *DPInst.xml*ファイルが含まれない**言語**要素。 ただし場合、 *DPInst.xml*ファイルが含まれます**言語**で明示的に指定されている言語のみの要素、**言語**要素が有効になっていると、すべてのその他の言語は暗黙的に無効になります。 すべての暗黙的に無効になっている言語を有効にするには設定、 **enableNotListedLanguages**を ON にフラグを含めることによって、 **enableNotListedLanguages**要素の子要素として、 **dpinst** XML 要素を使用して、または、 **/el** コマンド ライン スイッチ。

次のコード例に示します、 **enableNotListedLanguages**要素。

```cpp
<dpinst>
  ...
  <enableNotListedLanguages/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

 

 







---
title: legacyMode XML 要素
description: LegacyMode XML 要素は、未署名のドライバーとファイルが欠落しているドライバー パッケージをインストールする DPInst を構成するには、legacyMode フラグを設定する空要素です。
ms.assetid: a070551c-6053-42ba-873c-ac624afecfd0
keywords:
- legacyMode XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- legacyMode XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03a8bfe19b6ce5e545c6b2b8a17e540e85c6d235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571979"
---
# <a name="legacymode-xml-element"></a>legacyMode XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**LegacyMode** XML 要素が空の要素を設定する、 **legacyMode**未署名のドライバーをインストールする DPInst を構成するには、フラグと[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)です見つからないファイルがあります。

**要素タグ**

```cpp
<legacyMode>
```

**XML 属性**

なし

**要素情報**

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

 

**注釈**

既定では、DPInst インストールでのみ署名[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)と見つからないファイルがないドライバー パッケージ。 未署名のドライバ パッケージまたはファイルが欠落しているドライバー パッケージをそのまま使用する DPInst を構成する設定、 **legacyMode**を ON にフラグを含めることによって、 **legacyMode** の子要素として**dpinst** XML 要素またはを使用して、 **/lm** コマンド ライン スイッチ。

次のコード例に示します、 **legacyMode**要素。

```cpp
<dpinst>
  ...
  <legacyMode/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

 

 







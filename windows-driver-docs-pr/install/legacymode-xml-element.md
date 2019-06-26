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
ms.openlocfilehash: 1c8f23884ae01f2355438dcc0c78c824ef103508
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377674"
---
# <a name="legacymode-xml-element"></a>legacyMode XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**LegacyMode** XML 要素が空の要素を設定する、 **legacyMode**未署名のドライバーをインストールする DPInst を構成するには、フラグと[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)です見つからないファイルがあります。

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

既定では、DPInst インストールでのみ署名[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)と見つからないファイルがないドライバー パッケージ。 未署名のドライバ パッケージまたはファイルが欠落しているドライバー パッケージをそのまま使用する DPInst を構成する設定、 **legacyMode**を ON にフラグを含めることによって、 **legacyMode** の子要素として**dpinst** XML 要素またはを使用して、 **/lm** コマンド ライン スイッチ。

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

 

 







---
title: quietInstall XML 要素
description: quietInstall XML 要素
ms.assetid: 1151a68f-17c8-4852-9dc0-ab5dea9d58c6
keywords:
- quietInstall XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- quietInstall XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0ab0641646d788e02e1e65459e002842b4491a10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531072"
---
# <a name="quietinstall-xml-element"></a>quietInstall XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**QuietInstall** XML 要素が空の要素を設定する、 **quietInstall**フラグには、ウィザード ページおよびその他のほとんどのユーザー メッセージの表示を抑制する DPInst を構成します。

### <a name="element-tag"></a>**要素タグ**

```cpp
<quietInstall>
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

既定で、 **quietInstall**フラグが OFF に設定します。 設定することができます、 **quietInstall**を ON にフラグを含めることによって、 **quietInstall**要素 DPInst 記述子ファイル、またはを使用して、 **/q** コマンド ライン スイッチ。 **QuietInstall**フラグは、EULA ページのプレゼンスと連携し、 **suppressEulaPage**フラグ。

次のコード例に示します、 **quietInstall**要素

```cpp
<dpinst>
  ...
  <quietInstall/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

 

 







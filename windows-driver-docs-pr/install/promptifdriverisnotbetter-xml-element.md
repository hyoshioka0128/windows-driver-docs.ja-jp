---
title: promptIfDriverIsNotBetter XML 要素
description: promptIfDriverIsNotBetter XML 要素
ms.assetid: e5808c64-daa8-4aad-9a63-7ff79b0c2e49
keywords:
- promptIfDriverIsNotBetter XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- promptIfDriverIsNotBetter XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0a9c6d95db60d5cce48b0c27013bf199a58e249f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380470"
---
# <a name="promptifdriverisnotbetter-xml-element"></a>promptIfDriverIsNotBetter XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**PromptIfDriverIsNotBetter** XML 要素が空の要素を設定する、 **promptIfDriverIsNotBetter**フラグには、新しいドライバーが最適でない場合は、ダイアログ ボックスを表示する DPInst を構成します。デバイスに現在インストールされているドライバーよりものデバイス。 ダイアログ ボックスでは、このような状況のユーザーに通知し、新しいドライバーを使用したデバイスに現在インストールされているドライバーを置換するオプションを提供します。

### <a name="element-tag"></a>要素タグ

```cpp
<promptIfDriverIsNotBetter>
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

既定で、 **promptIfDriverIsNotBetter**フラグが OFF に設定します。 設定することができます、 **promptIfDriverIsNotBetter**を ON にフラグを含めることによって、 **promptIfDriverIsNotBetter**内の XML 要素を*DPInst.xml*ファイルまたはを使用して、 **/p** コマンド ライン スイッチ。

次のコード例に示します、 **promptIfDriverIsNotBetter**要素。

```cpp
<dpinst>
  ...
  <promptIfDriverIsNotBetter/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

 

 







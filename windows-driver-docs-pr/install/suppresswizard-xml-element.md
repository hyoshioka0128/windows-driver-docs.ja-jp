---
title: suppressWizard XML 要素
description: SuppressWizard XML 要素は、空の要素には、構成ウィザードのページと DPInst を生成するその他のユーザー メッセージを表示しないようにする DPInst suppressWizard フラグを設定します。
ms.assetid: fb72ff30-7d93-4531-9115-c299fabec7e7
keywords:
- suppressWizard XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- suppressWizard XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 36e775a68a1fadd56c48a71d7622109862418489
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385867"
---
# <a name="suppresswizard-xml-element"></a>suppressWizard XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**SuppressWizard** XML 要素が空の要素を設定する、 **suppressWizard**その DPInst には、構成ウィザードのページおよびその他のユーザー メッセージを表示しないようにする DPInst フラグ生成されます。

**要素タグ**

```cpp
<suppressWizard>
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

既定で、 **suppressWizard**フラグが OFF に設定します。 設定することができます、 **suppressWizard**を ON にフラグを含めることによって、 **suppressWizard** XML 要素の子要素として、 **dpinst** DPInst 記述子ファイル、またはを使用して XML 要素 **/sw** コマンド ライン スイッチ。 **SuppressWizard**フラグの連携、 **suppressEulaPage**フラグ。

次のコード例に示します、 **suppressWizard**要素。

```cpp
<dpinst>
  ...
  <suppressWizard/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

 

 







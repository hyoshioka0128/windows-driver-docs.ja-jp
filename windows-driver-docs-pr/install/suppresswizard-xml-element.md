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
ms.openlocfilehash: 72c24e2bbd3ea296555b4563294ae229dd022233
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339636"
---
# <a name="suppresswizard-xml-element"></a>suppressWizard XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

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

 

 







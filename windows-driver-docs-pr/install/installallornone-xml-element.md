---
title: installAllOrNone XML 要素
description: installAllOrNone XML 要素
ms.assetid: f5634def-c9a1-45db-88ce-f652171d19c9
keywords:
- installAllOrNone XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- installAllOrNone XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f14b87c0f216509f9c3fd34951c746bef0326d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370020"
---
# <a name="installallornone-xml-element"></a>installAllOrNone XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**InstallAllOrNone** XML 要素が空の要素を設定する、 **installAllOrNone**でドライバーをインストールする DPInst を構成するには、フラグ、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)のみすべてのインストール パッケージにドライバー パッケージをインストールする場合、または場合、すべてのドライバー パッケージ グループでのドライバー パッケージをインストールすることができます。

### <a name="element-tag"></a>**要素タグ**

```cpp
<installAllOrNone>
```

### <a name="xml-attributes"></a>**XML 属性**

なし

### <a name="element-information"></a>**要素情報**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>親要素</strong></p></td>
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong> </a>または<a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>グループ</strong></a></p></td>
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

既定で、 **installAllOrNone**フラグが OFF に設定します。 設定する、 **installAllOrNone** ON のすべてのフラグ、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)、含めるドライバー パッケージのグループに含めて、 **installAllOrNone**子要素として要素を**dpinst** 、XML 要素を使用して、または、 **/a** コマンド ライン スイッチ。 設定する、 **installAllOrNone**の特定のドライバー パッケージのグループにのみフラグを ON に、インクルード、 **installAllOrNone**要素に対応する子要素として**グループ**XML 要素。

次のコード例に示します、 **installAllOrNone**要素の子要素である、 **dpinst**要素。

```cpp
<dpinst>
  ...
  <installAllOrNone/>
  ...
</dpinst>
```

次のコード例に示します、 **installAllOrNone**要素の子要素である、**グループ**要素。

```cpp
<dpinst>
  ...
  <group>
    <package path="DirAbc\Abc.inf" /> 
    <package path="DirDef\Def.inf" /> 
    <installAllOrNone/>
  <group/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

[**グループ**](group-xml-element.md)

 

 







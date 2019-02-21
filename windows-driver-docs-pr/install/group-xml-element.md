---
title: XML 要素をグループ化します。
description: XML 要素をグループ化します。
ms.assetid: 8035fd60-065c-4282-a18c-34e6a5201e56
keywords:
- グループの XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- group XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a9e6b6e2e44ca75a145f027ec77b1d2da2cab0b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532063"
---
# <a name="group-xml-element"></a>XML 要素をグループ化します。


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**グループ**XML 要素の順序付きのコレクションを指定する[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)その DPInst では、ドライバー パッケージ グループとして処理します。

### <a name="element-tag"></a>要素タグ

```cpp
<group>
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
<td align="left"><p><a href="package-xml-element.md" data-raw-source="[&lt;strong&gt;package&lt;/strong&gt;](package-xml-element.md)"><strong>パッケージ</strong></a> (0 個以上)</p>
<p><a href="installallornone-xml-element.md" data-raw-source="[&lt;strong&gt;installAllOrNone&lt;/strong&gt;](installallornone-xml-element.md)"><strong>installAllOrNone</strong> </a> (0 個または 1)</p>
<p><a href="suppressaddremoveprograms-xml-element.md" data-raw-source="[&lt;strong&gt;suppressAddRemovePrograms&lt;/strong&gt;](suppressaddremoveprograms-xml-element.md)"><strong>suppressAddRemovePrograms</strong> </a> (0 個または 1)</p></td>
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

次のコード例に示します、**グループ**要素を含む 2 つ[ **XML 要素をパッケージ化**](package-xml-element.md)と[ **installAllOrNoneXML 要素**](installallornone-xml-element.md)します。 例では、**グループ**要素は、"Abc"を処理するために DPInst を構成します。[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)と"Def"ドライバー パッケージをグループとして。 **InstallAllOrNone** XML 要素は、両方のドライバーをインストールする場合にのみ、ドライバー パッケージ グループで、ドライバー パッケージをインストールする DPInst を構成します。

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

[**installAllOrNone**](installallornone-xml-element.md)

[**パッケージ**](package-xml-element.md)

[**suppressAddRemovePrograms**](suppressaddremoveprograms-xml-element.md)

 

 







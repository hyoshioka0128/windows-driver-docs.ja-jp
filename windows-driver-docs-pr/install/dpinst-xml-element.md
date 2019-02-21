---
title: dpinst XML 要素
description: dpinst XML 要素
ms.assetid: d825afb4-a459-4b69-93cb-db57adab3c80
keywords:
- dpinst XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- dpinst XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 85524f42e57c15a7aa08c38ce0ae0878b9f56ce1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553988"
---
# <a name="dpinst-xml-element"></a>dpinst XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**Dpinst** XML 要素は、ドライバーのインストールをカスタマイズする子要素を含む DPInst 記述子ファイルの XML ルート要素。

### <a name="element-tag"></a>要素タグ

```cpp
<dpinst>
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
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p><a href="enablenotlistedlanguages-xml-element.md" data-raw-source="[&lt;strong&gt;enableNotListedLanguages&lt;/strong&gt;](enablenotlistedlanguages-xml-element.md)"><strong>enableNotListedLanguages</strong> </a> (0 個または 1)</p>
<p><a href="deletebinaries-xml-element.md" data-raw-source="[&lt;strong&gt;deleteBinaries&lt;/strong&gt;](deletebinaries-xml-element.md)"><strong>deleteBinaries</strong> </a> (0 個または 1)</p>
<p><a href="forceifdriverisnotbetter-xml-element.md" data-raw-source="[&lt;strong&gt;forceIfDriverIsNotBetter&lt;/strong&gt;](forceifdriverisnotbetter-xml-element.md)"><strong>forceIfDriverIsNotBetter</strong> </a> (0 個または 1)</p>
<p><a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>グループ</strong></a> (0 個以上)</p>
<p><a href="headerpath-xml-element.md" data-raw-source="[&lt;strong&gt;headerPath&lt;/strong&gt;](headerpath-xml-element.md)"><strong>headerPath</strong> </a> (0 個または 1)</p>
<p><a href="icon-xml-element.md" data-raw-source="[&lt;strong&gt;icon&lt;/strong&gt;](icon-xml-element.md)"><strong>アイコン</strong></a> (0 個または 1)</p>
<p><a href="installallornone-xml-element.md" data-raw-source="[&lt;strong&gt;installAllOrNone&lt;/strong&gt;](installallornone-xml-element.md)"><strong>installAllOrNone</strong> </a> (0 個または 1)</p>
<p><a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"><strong>言語</strong></a> (0 個以上)</p>
<p><a href="legacymode-xml-element.md" data-raw-source="[&lt;strong&gt;legacyMode&lt;/strong&gt;](legacymode-xml-element.md)"><strong>legacyMode</strong> </a> (0 個または 1)</p>
<p><a href="promptifdriverisnotbetter-xml-element.md" data-raw-source="[&lt;strong&gt;promptIfDriverIsNotBetter&lt;/strong&gt;](promptifdriverisnotbetter-xml-element.md)"><strong>promptIfDriverIsNotBetter</strong> </a> (0 個または 1)</p>
<p><a href="quietinstall-xml-element.md" data-raw-source="[&lt;strong&gt;quietInstall&lt;/strong&gt;](quietinstall-xml-element.md)"><strong>quietInstall</strong> </a> (0 個または 1)</p>
<p><a href="scanhardware-xml-element.md" data-raw-source="[&lt;strong&gt;scanHardware&lt;/strong&gt;](scanhardware-xml-element.md)"><strong>scanHardware</strong> </a> (0 個または 1)</p>
<p><a href="search-xml-element.md" data-raw-source="[&lt;strong&gt;search&lt;/strong&gt;](search-xml-element.md)"><strong>検索</strong></a> (0 個以上)</p>
<p><a href="suppressaddremoveprograms-xml-element.md" data-raw-source="[&lt;strong&gt;suppressAddRemovePrograms&lt;/strong&gt;](suppressaddremoveprograms-xml-element.md)"><strong>suppressAddRemovePrograms</strong> </a> (0 個または 1)</p>
<p><a href="watermarkpath-xml-element.md" data-raw-source="[&lt;strong&gt;watermarkPath&lt;/strong&gt;](watermarkpath-xml-element.md)"><strong>watermarkPath</strong> </a> (0 個または 1)</p></td>
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

次のコード例は、後に、XML 宣言要素を示して、 **dpinst**要素、0 個以上の子要素が含まれます。

```cpp
<?xml version="1.0" ?>
<dpinst>
  ...
</dpinst>
```

**注**  重複する子要素が許可されないため、各**検索**子要素と**言語**の要素を**dpinst**要素は一意である必要があります。

 

## <a name="see-also"></a>関連項目


[**deleteBinaries**](deletebinaries-xml-element.md)

[**enableNotListedLanguages**](enablenotlistedlanguages-xml-element.md)

[**forceIfDriverIsNotBetter**](forceifdriverisnotbetter-xml-element.md)

[**グループ**](group-xml-element.md)

[**headerPath**](headerpath-xml-element.md)

[**icon**](icon-xml-element.md)

[**installAllOrNone**](installallornone-xml-element.md)

[**言語**](language-xml-element.md)

[**legacyMode**](legacymode-xml-element.md)

[**promptIfDriverIsNotBetter**](promptifdriverisnotbetter-xml-element.md)

[**quietInstall**](quietinstall-xml-element.md)

[**scanHardware**](scanhardware-xml-element.md)

[**search**](search-xml-element.md)

[**suppressAddRemovePrograms**](suppressaddremoveprograms-xml-element.md)

[**watermarkPath**](watermarkpath-xml-element.md)

 

 







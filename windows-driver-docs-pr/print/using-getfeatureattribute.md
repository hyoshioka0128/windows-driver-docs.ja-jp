---
title: GetFeatureAttribute の使用
description: GetFeatureAttribute の使用
ms.assetid: e5050cb1-c178-405d-bb0e-fd7827198bca
keywords:
- GetFeatureAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 934b53fe996ec01faf25c370684262efb6ac0f07
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463972"
---
# <a name="using-getfeatureattribute"></a>GetFeatureAttribute の使用





この関数は、PPD 機能のみサポートされます。 特定の属性が使用できない場合**GetFeatureAttribute**返します E\_INVALIDARG します。

次の表に、 *pdwDataType*パラメーターの値には、 [ **EATTRIBUTE\_DATATYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff548692)列挙型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能の属性</th>
<th>出力パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DisplayName</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>pbData</em>: 機能キーワード名の翻訳文字列の null で終わる Unicode 文字列</p>
<p><em></em>pcbNeeded</em>: Unicode 文字列のバイト数が指す<em>pbData</em> (null 終端文字を含む)</p>
<p>この機能の属性はすべて PPD 機能を利用可能な<strong>EnumFeatures</strong>返すことができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefaultOption</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: 既定のオプションのキーワード名の null で終わる ASCII 文字列</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>この機能の属性はすべて PPD 機能を利用可能な<strong>EnumFeatures</strong>返すことができます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OpenUIType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: 次の種類のいずれかを含む null で終わる ASCII 文字列。"PickOne"、"PickMany"、"Boolean"。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>この機能の属性はすべて PPD 機能を利用可能な<strong>EnumFeatures</strong>返すことができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenGroupType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:PPD の内で定義されている機能の"</em>OpenGroup:InstallableOptions.<em>CloseGroup:InstallableOptions"ペア"InstallableOptions"の null で終わる ASCII 文字列が返されます。 その他の機能 (これで、null 終端記号だけを持つ) 空の ASCII 文字列が返されます。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>この機能の属性はすべて PPD に利用可能な機能を<strong>EnumFeatures</strong>返すことができます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p><em>pdwDataType: kADT_LONG</p>
<p><em></em>pbData</em>: PPD のによって指定された相対順序<em>OrderDependency または<em>NonUIOrderDependency キーワードは、この機能をします。 これらのキーワードの最初のパラメーターは、長整数型に変換され、返される実数であることを確認します。</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(LONG)</p>
<p>この属性がある PPD 機能でのみ使用できますが、 <em>OrderDependency または *、PPD で NonUIOrderDependency エントリと、エントリ optionKeyword が省略されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: セクション名を次のいずれかを含む null で終わる ASCII 文字列。"ExitServer"、「プロローグ」、"DocumentSetup"、"PageSetup"、"JCLSetup"または"AnySetup"。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>この属性がある PPD 機能でのみ使用できますが、* OrderDependency または *、PPD で NonUIOrderDependency エントリと、エントリ optionKeyword が省略されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





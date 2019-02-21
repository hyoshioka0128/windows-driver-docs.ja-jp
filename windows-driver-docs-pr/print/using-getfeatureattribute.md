---
title: GetFeatureAttribute を使用します。
description: GetFeatureAttribute を使用します。
ms.assetid: e5050cb1-c178-405d-bb0e-fd7827198bca
keywords:
- GetFeatureAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f8b02e4f82a0fa0254c40b8b5a72d98bde86ae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557467"
---
# <a name="using-getfeatureattribute"></a>GetFeatureAttribute を使用します。





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
<p><em>pbData</em>: 機能のキーワード名の null で終わる Unicode 文字列&#39;s 翻訳文字列</p>
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
<p><em>pbData</em>: 次の種類のいずれかを含む null で終わる ASCII 文字列。&quot;PickOne&quot;、 &quot;PickMany&quot;、&quot;ブール&quot;します。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>この機能の属性はすべて PPD 機能を利用可能な<strong>EnumFeatures</strong>返すことができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenGroupType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:PPD 内で定義されている機能の&#39;s &quot; </em>OpenGroup:InstallableOptions.<em>CloseGroup:InstallableOptions&quot;とペアに null で終わる ASCII 文字列の&quot;InstallableOptions&quot;が返されます。 その他の機能 (これで、null 終端記号だけを持つ) 空の ASCII 文字列が返されます。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>この機能の属性はすべて PPD に利用可能な機能を<strong>EnumFeatures</strong>返すことができます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p><em>pdwDataType: kADT_LONG</p>
<p><em></em>pbData</em>: PPD で指定された相対順序&#39;s <em>OrderDependency または<em>NonUIOrderDependency キーワードは、この機能をします。 これらのキーワードの最初のパラメーターは、長整数型に変換され、返される実数であることを確認します。</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(LONG)</p>
<p>この属性がある PPD 機能でのみ使用できますが、 <em>OrderDependency または *、PPD で NonUIOrderDependency エントリと、エントリ optionKeyword が省略されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: セクション名を次のいずれかを含む null で終わる ASCII 文字列。&quot;ExitServer&quot;、&quot;プロローグ&quot;、 &quot;DocumentSetup&quot;、 &quot;PageSetup&quot;、 &quot;JCLSetup&quot;、または&quot;AnySetup&quot;.</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>この属性がある PPD 機能でのみ使用できますが、* OrderDependency または *、PPD で NonUIOrderDependency エントリと、エントリ optionKeyword が省略されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: GetFeatureAttribute の使用
description: GetFeatureAttribute の使用
ms.assetid: e5050cb1-c178-405d-bb0e-fd7827198bca
keywords:
- GetFeatureAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89cc57d697891557e9848a7f0c1cf83e0eb38950
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843617"
---
# <a name="using-getfeatureattribute"></a>GetFeatureAttribute の使用





この関数は、PPD 機能に対してのみサポートされています。 特定の属性が使用できない場合、 **Getfeatureattribute**は E\_invalidarg を返します。

次の表では、 *pdwDataType*パラメーターは、 [**EATTRIBUTE\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype)列挙型の値を受け取ります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能属性</th>
<th>出力パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DisplayName</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>Pbdata</em>: 機能キーワード名の翻訳文字列の null で終わる Unicode 文字列</p>
<p>pcbNeeded な</em>: <em>Pbdata</em>が指す Unicode 文字列のバイト数 (null 終端文字を含む)</p>
<p>この機能属性は、 <strong>Enumfeatures</strong>が返すことができるすべての PPD 機能で使用できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefaultOption</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: 既定の option キーワード名の null で終わる ASCII 文字列</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (null 終端文字を含む)</p>
<p>この機能属性は、 <strong>Enumfeatures</strong>が返すことができるすべての PPD 機能で使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OpenUIType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: 次のいずれかの型を含む null で終わる ASCII 文字列: "1 つをピックする"、"複数の値を指定する"、"Boolean"。</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (null 終端文字を含む)</p>
<p>この機能属性は、 <strong>Enumfeatures</strong>が返すことができるすべての PPD 機能で使用できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenGroupType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: PPD の "</em>opengroup: installableoptions... <em>Closegroup: installableoptions" ペアで定義された機能については、null で終わる ASCII 文字列 "InstallableOptions" が返されます。 その他の機能については、null 終端文字のみを含む空の ASCII 文字列が返されます。</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (null 終端文字を含む)</p>
<p>この機能属性は、 <strong>Enumfeatures</strong>が返すことができる任意の PPD 機能で使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p><em>pdwDataType: kADT_LONG</p>
<p>pbData</em>: この機能のために、PPD の <em>OrderDependency または <em>NonUIOrderDependency キーワードによって指定された相対順序。 これらのキーワードの最初のパラメーターは、LONG に変換されて返される実数であることに注意してください。</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(LONG)</p>
<p>この属性は、ppd に <em>OrderDependency または * NonUIOrderDependency エントリを持つ PPD 機能に対してのみ使用できます。この場合は、optionKeyword を省略します。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: "exitserver"、"プロローグ"、"documentsetup"、"PageSetup"、"JCLSetup"、"anysetup" のいずれかのセクション名を含む null で終わる ASCII 文字列。</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (null 終端文字を含む)</p>
<p>この属性は、ppd に * OrderDependency または * NonUIOrderDependency エントリを持つ PPD 機能に対してのみ使用できます。また、entry オプションを省略します。</p></td>
</tr>
</tbody>
</table>

 

 

 





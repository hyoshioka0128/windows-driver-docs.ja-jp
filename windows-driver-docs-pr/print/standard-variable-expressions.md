---
title: 標準変数式
description: 標準変数式
ms.assetid: b77c6b88-9ef2-4485-b77c-50acb21e13b9
keywords:
- プリンターが WDK Unidrv、文字列をコマンドします。
- コマンド文字列を WDK Unidrv
- WDK Unidrv 文字列
- 標準的な変数式 WDK Unidrv
- max_repeat
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7117dd8b674d5877b75d6c5ee677b2f522813910
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581303"
---
# <a name="standard-variable-expressions"></a>標準変数式





コマンド文字列で引数を指定する場合は、式として、引数の値を指定できます。 この式は、の現在の値を使用して操作を実行できる、[標準変数](standard-variables.md)します。 コマンド文字列内の標準的な各変数式は、中かっこ ({、}) で区切られます。

標準的な変数式は、次のコンポーネントの組み合わせで構成できます。

-   0、1 つ、以上[標準的な変数](standard-variables.md)

-   整数[数値](numeric-values.md)

-   式の演算子

標準的な変数式は、埋め込みのマクロの参照を含めることはできません。

次の表では、式の演算子が含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>演算子</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Val1</em><strong>+</strong><em>Val2</em></p></td>
<td><p>加算します。</p></td>
</tr>
<tr class="even">
<td><p><em>Val1</em><strong>-</strong><em>Val2</em></p></td>
<td><p>減算します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Val1</em><strong>/</strong><em>Val2</em></p></td>
<td><p>除算します。</p></td>
</tr>
<tr class="even">
<td><p><em>Val1</em><strong>*</strong><em>Val2</em></p></td>
<td><p>乗算します。</p></td>
</tr>
<tr class="odd">
<td><p><em>Val1</em><strong>MOD</strong><em>Val2</em></p></td>
<td><p>剰余。 値が除算した剰余<em>Val1</em>によって<em>Val2</em>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>max</strong> ( <em>Val1</em> 、 <em>Val2</em> )</p></td>
<td><p>最大値。 値は、最大<em>Val1</em>と<em>Val2</em>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>max_repeat</strong> ( <em>Val1</em> )</p></td>
<td><p>参照してください、 <strong>max_repeat を使用して</strong>セクション。</p></td>
</tr>
<tr class="even">
<td><p><strong>min</strong> ( <em>Val1</em> 、 <em>Val2</em> )</p></td>
<td><p>最小値。 値の最小値は、 <em>Val1</em>と<em>Val2</em>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>( )</strong></p></td>
<td><p>優先順位の演算子。 使用しない場合は、C 言語の優先順位が使用されます。</p></td>
</tr>
</tbody>
</table>

 

標準的な変数式では、標準的な変数に割り当てられた値は変更しないでください。 計算された値がで指定された形式を使用して、エスケープ シーケンスは、配置、[コマンド文字列引数の型](command-string-argument-types.md)指定子。

### <a href="" id="ddk-using-max-repeat-gg"></a>Max を使用する\_繰り返します

使用**max\_繰り返します**例をわかりやすく説明します。 GPD ファイルには、次のエントリが含まれているとします。

```cpp
*Command:CmdXMoveRelRight{*Cmd:"<1B>["%d[0,9600]{max_repeat((DestXRel/4))}"a"}
```

このコマンドには、型の 1 つの引数が含まれています。 **%d**します。 引数の範囲指定も含まれています。 Unidrv は、このコマンドをプリンターに送信するたびに、DestXRel/4 を計算します。 最初し、指定された範囲内にあるかどうかを決定します。 計算された値が 9600 よりも大きい場合は、Unidrv コマンドを送信、繰り返し 9600、指定した値が送信されるまでの最大値。 したがって DestXRel/4 では、20,000 と等しい、Unidrv は、次のコマンドを送信します。

```cpp
<1B>[9600
<1B>[9600
<1B>[800
```

**Max\_繰り返します**演算子は、次の条件が満たされた場合にのみ使用できます。

-   コマンド文字列には、1 つの引数のみが含まれています。

-   引数には、範囲指定が含まれています。

 

 





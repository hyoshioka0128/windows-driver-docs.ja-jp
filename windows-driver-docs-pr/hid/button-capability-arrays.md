---
title: ボタンの機能の配列
description: ボタンの機能の配列
ms.assetid: 139324e5-4d46-4d00-9f5a-fd0313fc109a
keywords:
- WDK の HID ボタンの機能を配列します。
- WDK の HID 配列
- コレクションの WDK を非表示の機能
- WDK の HID ボタンの使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7f629555bf78105b0ad0f193b83eb88ee81b41b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529277"
---
# <a name="button-capability-arrays"></a>ボタンの機能の配列





A*ボタン機能配列*でサポートされているボタンの使用状況に関する情報を格納、[最上位のコレクション](top-level-collections.md)HID レポートの特定の種類。 コレクションの機能に関する情報が含まれているその[ **HIDP\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)構造体。

ユーザー モード アプリケーションまたはカーネル モード ドライバーは、次のいずれかを使用して[HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)ボタンの機能情報を取得します。

-   [**HidP\_GetButtonCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539707)レポートの指定した型に含まれるすべてのボタン使用法を説明するボタンの機能の配列を返します。

-   [**HidP\_GetSpecificButtonCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539733)呼び出し元が指定した使用状況] ページ、使用状況の ID を返します、ボタンの機能情報をフィルター処理と[リンク コレクション](link-collections.md)します。

ボタンの機能の配列に含まれる[ **HIDP\_ボタン\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539693)うちそれぞれに関する次の情報を格納する構造を[するHID使用法](hid-usages.md)または[使用範囲](hid-usages.md#usage-range):

-   使用状況または使用状況の範囲の使用状況 ページ

-   ボタンのデータを含む、レポートのレポート ID

-   使用状況 ID または使用状況の範囲

-   使用方法は、かどうかを示すフラグを[別名の使用状況](hid-usages.md#aliased-usages)

-   使用状況や使用状況の範囲を含むリンク コレクション

-   文字列記述子と使用状況や使用状況の範囲に関連付けられている指定子 (指定子のインデックスの項目と文字列のインデックスの項目を参照してください)

-   [データのインデックス](data-indices.md)HID パーサーが使用または使用状況の範囲に割り当てられています。

一般に、次の条件は、ボタンの機能の配列で説明されているすべての使用状況の保持します。

-   各機能の構造は、1 つの使用状況または変数の主な項目または配列の主な項目に関連付けられている使用量の範囲を表します。

-   エイリアスの使用法は、変数の主な項目で使用できます。 配列の項目に関連付けられている使用量は、エイリアスにすることはできません。 使用状況の範囲は、エイリアスにすることはできません。

-   HID パーサーでは、使用法の最低限必要な数のみを使用して、使用状況を各ボタンに割り当てます。 パーサーでは、使用状況レポート記述子で指定されている順序で割り当てられます。 必要でない使用状況のレポート記述子は破棄されます。 ボタンの機能の配列では、破棄された使用状況に関する情報は含まれません。

-   機能の配列には変数の項目に指定された使用法の数が、項目内のボタンの数よりも小さい場合は、ボタン使用法 (、最終使用、変数がメインのレポート記述子で指定された 1 つを記述する 1 つだけの機能の構造体が含まれています項目の場合)。 ただしを参照してください[値配列の使用状況](value-capability-arrays.md#usage-value-array)使用方法については、レポートの値を 1 より大きいカウントです。

-   HID パーサーでは、機能の配列で説明されている各使用法に一意のデータのインデックスを割り当てます。

次のトピックでは、機能の構造を整理し、ボタンの機能の配列に設定する方法について説明します。

[変数の主な項目でボタンの使用](#button-usages-in-a-variable-main-item)

[配列の主な項目でボタンの使用](#button-usages-in-an-array-main-item)

### <a href="" id="button-usages-in-a-variable-main-item"></a> 変数の主な項目でボタンの使用

各[使用状況](hid-usages.md)または[使用状況の範囲](hid-usages.md#usage-range)が指定されているレポートの記述子がボタンの機能の配列で、独自機能の構造によって記述されます。

**IsAlias**機能の構造体のメンバーのセットを指定に使用されます*n*次のように、別名の使用法。

-   **IsAlias**に設定されている**TRUE**最初*n*-1 機能の構造体の機能の配列に追加します。 **IsAlias**設定**FALSE**で、 *n*th 機能の構造体。 推奨される使用方法は、シーケンスの最後の別名の使用状況です。

アプリケーション、ドライバーは、どのボタンの使用方法は、このようなシーケンスをスキャンしてエイリアスは判断できます。

次の表では、次の 3 つの別名の使用状況の例をまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>レポート記述子の別名の使用状況の順序</th>
<th>機能の配列内の使用状況の順序</th>
<th>IsAlias メンバー値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用率 1</p></td>
<td><p>使用状況 3</p></td>
<td><p><strong>TRUE</strong></p></td>
</tr>
<tr class="even">
<td><p>使用量 2</p></td>
<td><p>使用量 2</p></td>
<td><p><strong>TRUE</strong></p></td>
</tr>
<tr class="odd">
<td><p>使用状況 3</p></td>
<td><p>使用率 1</p></td>
<td><p><strong>FALSE</strong></p></td>
</tr>
</tbody>
</table>

 

使用法とデータのインデックスは相互参照する方法については、次を参照してください。[データのインデックス](data-indices.md)します。

### <a href="" id="button-usages-in-an-array-main-item"></a> 配列の主な項目でボタンの使用

各[使用状況](hid-usages.md)または[使用範囲](hid-usages.md#usage-range)ボタン機能の配列で、独自機能の構造によって、レポートで指定したボタン配列主な項目の記述子が説明されています。 機能の配列に、機能の構造を追加する順序は、主な項目の使用法を指定する順の逆です。

HID パーサーを割り当てます、[データ インデックス](data-indices.md)の使用状況がレポート記述子で指定されている順序で配列の項目に関連付けられている各使用法をします。 たとえば、次の表は、一連のレポート記述子、および使用法で指定されている、使用状況と機能の配列で指定されている、データのインデックスの対応を示します。 (この表で、 *n*は配列の項目に関連付けられている最初の使用にパーサーを代入する最初のデータ インデックスです)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用状況レポート記述子の順番</th>
<th>機能の配列内の使用状況の順序</th>
<th>DataIndex または DatatIndexMax に DataIndexMin から</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用率 1</p></td>
<td><p>範囲 2 の使用状況</p></td>
<td><p><em>n</em>を + 7 <em>n</em>+8</p></td>
</tr>
<tr class="even">
<td><p>(4 の使用法) の使用状況の範囲 1</p></td>
<td><p>使用量 2</p></td>
<td><p><em>n</em>+5</p></td>
</tr>
<tr class="odd">
<td><p>使用量 2</p></td>
<td><p>使用状況の範囲 1</p></td>
<td><p><em>n</em>を +1 <em>n</em>+4</p></td>
</tr>
<tr class="even">
<td><p>(2 つの使用法) の使用範囲 2</p></td>
<td><p>使用率 1</p></td>
<td><p><em>n</em></p></td>
</tr>
</tbody>
</table>

 

 

 





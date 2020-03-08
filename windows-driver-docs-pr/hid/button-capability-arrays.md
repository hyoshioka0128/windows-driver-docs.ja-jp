---
title: ボタン機能配列
description: ボタン機能配列
ms.assetid: 139324e5-4d46-4d00-9f5a-fd0313fc109a
keywords:
- ボタン機能配列 WDK HID
- アレイ WDK HID
- 機能 WDK HID コレクション
- ボタンの使用法 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 851ec3f35cf3d147fc872c15989b5003fcce8d4e
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78854025"
---
# <a name="button-capability-arrays"></a>ボタン機能配列





*ボタン機能の配列*には、特定の種類の HID レポートの[最上位のコレクション](top-level-collections.md)でサポートされているボタンの使用法に関する情報が含まれています。 コレクションの機能に関する情報は、 [**Hidp\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体に含まれています。

ユーザーモードのアプリケーションまたはカーネルモードドライバーは、次のいずれかの[HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用して、ボタンの機能情報を取得します。

-   [**Hidp\_GetButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)は、指定されたレポートの種類に含まれるすべてのボタンの使用法を記述するボタン機能の配列を返します。

-   [**Hidp\_Get固有の Buttoncaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificbuttoncaps)は、呼び出し元が指定した使用状況ページ、使用 ID、および[リンクコレクション](link-collections.md)によって返されるボタン機能情報をフィルター処理します。

ボタン機能配列には、 [**Hidp\_button\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_button_caps)構造体が含まれています。それぞれには、 [HID の使用法](hid-usages.md)または[使用状況の範囲](hid-usages.md#usage-range)に関する次の情報が含まれています。

-   使用状況または使用状況の範囲の [使用状況] ページ

-   ボタンデータを含むレポートのレポート ID

-   使用状況 ID または使用状況の範囲

-   使用法が[別名で使用](hid-usages.md#aliased-usages)されるかどうかを示すフラグ

-   使用状況または使用状況の範囲を含むリンクコレクション

-   使用量または使用範囲に関連付けられている文字列記述子と指定子 (「指定子インデックス項目」および「文字列インデックス項目」を参照)

-   HID パーサーによって使用状況または使用状況の範囲に割り当てられた[データインデックス](data-indices.md)

一般に、ボタン機能配列で記述されているすべての使用について、次の条件が保持されます。

-   各機能構造は、変数のメイン項目または配列のメイン項目に関連付けられている1つの使用状況または使用状況の範囲を表します。

-   エイリアス化された使用法は、変数のメイン項目と共に使用できます。 配列項目に関連付けられている使用法にエイリアスを付けることはできません。 使用範囲のエイリアスを指定することはできません。

-   HID パーサーは、必要最小限の使用回数のみを使用して、各ボタンに使用状況を割り当てます。 パーサーは、使用法をレポート記述子で指定されている順序で割り当てます。 不要なレポート記述子での使用は破棄されます。 ボタン機能の配列には、破棄された使用法に関する情報は含まれていません。

-   変数項目に指定された使用量が項目内のボタン数よりも少ない場合、機能配列には、1つのボタンの使用法を記述する機能構造が1つだけ含まれます (これは、最初に変数のレポート記述子に指定された最後の使用方法です)。項目)。 ただし、レポート数が1より大きい使用状況値の詳細については、「[使用状況値の配列](value-capability-arrays.md#usage-value-array)」を参照してください。

-   HID パーサーは、機能配列に記述されている各使用方法に一意のデータインデックスを割り当てます。

次のトピックでは、ボタン機能配列での機能構造の編成方法と設定方法について説明します。

[変数のメイン項目でのボタンの使用法](#button-usages-in-a-variable-main-item)

[配列のメイン項目でのボタンの使用法](#button-usages-in-an-array-main-item)

### <a href="" id="button-usages-in-a-variable-main-item"></a>変数のメイン項目でのボタンの使用法

レポート記述子に指定されている[使用状況](hid-usages.md)または[使用状況の範囲](hid-usages.md#usage-range)はそれぞれ、ボタン機能の配列で独自の機能構造によって記述されます。

機能構造体の**Isalias**メンバーは、次のように*n 個*の別名の使用を指定するために使用されます。

-   **Isalias**は、機能配列に追加された最初の*n*-1 機能構造体で**TRUE**に設定されています。 *N*番目の機能構造で**Isalias**が**FALSE**に設定されています。 優先される使用方法は、シーケンス内で最後にエイリアス化された使用方法です。

アプリケーションまたはドライバーは、そのようなシーケンスをスキャンすることで、どのボタンの使用方法がエイリアス化されているかを判断できます。

次の表に、エイリアス化された3つの使用例の概要を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>レポート記述子での別名使用順序</th>
<th>機能配列の使用順序</th>
<th>IsAlias メンバーの値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用法1</p></td>
<td><p>使用量3</p></td>
<td><p><strong>本来</strong></p></td>
</tr>
<tr class="even">
<td><p>使用状況2</p></td>
<td><p>使用状況2</p></td>
<td><p><strong>本来</strong></p></td>
</tr>
<tr class="odd">
<td><p>使用量3</p></td>
<td><p>使用法1</p></td>
<td><p><strong>FALSE</strong></p></td>
</tr>
</tbody>
</table>

 

使用状況とデータインデックスを相互参照する方法については、「[データインデックス](data-indices.md)」を参照してください。

### <a href="" id="button-usages-in-an-array-main-item"></a>配列のメイン項目でのボタンの使用法

レポート記述子に指定されているボタン配列のメイン項目の[使用状況](hid-usages.md)または[使用状況の範囲](hid-usages.md#usage-range)はそれぞれ、ボタン機能配列で独自の機能構造によって記述されます。 機能構造が機能配列に追加される順序は、メイン項目に対して使用される順序と逆になります。

HID パーサーは、配列項目に関連付けられている各使用状況に、レポート記述子で指定されている順序で[データインデックス](data-indices.md)を割り当てます。 たとえば、次の表は、レポート記述子で指定されている一連の使用方法と、機能配列で指定されている使用状況とデータインデックスとの対応を示しています。 (この表では、 *n*は、配列項目に関連付けられた最初の使用状況にパーサーが割り当てた最初のデータインデックスです)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>レポート記述子の使用順序</th>
<th>機能配列の使用順序</th>
<th>DataIndex または DataIndexMin から DatatIndexMax へ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用法1</p></td>
<td><p>使用範囲2</p></td>
<td><p><em>n</em>+ 7 から<em>n</em>+ 8</p></td>
</tr>
<tr class="even">
<td><p>使用範囲 1 (4 使用)</p></td>
<td><p>使用状況2</p></td>
<td><p><em>n</em>+ 5</p></td>
</tr>
<tr class="odd">
<td><p>使用状況2</p></td>
<td><p>使用範囲1</p></td>
<td><p><em>n</em>+ 1 から<em>n</em>+ 4 まで</p></td>
</tr>
<tr class="even">
<td><p>使用範囲 2 (使用量 2)</p></td>
<td><p>使用法1</p></td>
<td><p><em>n</em></p></td>
</tr>
</tbody>
</table>

 

 

 





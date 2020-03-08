---
title: 値機能配列
description: 値機能配列
ms.assetid: d447dda6-a1e5-4e57-b06f-f79f8662c236
keywords:
- 値機能配列 WDK HID
- アレイ WDK HID
- 機能 WDK HID コレクション
- 使用状況値配列 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2ce4b80fc5bacd946381a1c9fe975690a5106ef
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78854021"
---
# <a name="value-capability-arrays"></a>値機能配列





*値機能配列*には、特定の種類の HID レポートの[最上位レベルのコレクション](top-level-collections.md)でサポートされている値の使用法に関する情報が含まれています。 コレクションの値機能配列に関する情報は、 [**Hidp\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体に含まれています。

ユーザーモードのアプリケーションまたはカーネルモードドライバーは、次のいずれかの[HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用して、ボタンの機能情報を取得します。

-   [**Hidp\_GetValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)は、呼び出し元が指定したレポートの種類に含まれるすべての値を記述する値機能配列を返します。

-   [**Hidp\_GetSpecificValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificvaluecaps)は、呼び出し元が指定した使用状況ページ、使用状況、リンクコレクション、およびレポートの種類によって返される値機能情報をフィルター処理します。

値機能配列には、 [**Hidp\_値\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps)構造体が含まれており、それぞれが[HID の使用法](hid-usages.md)または[使用状況の範囲](hid-usages.md#usage-range)に関する次の情報を記述します。

-   使用状況または使用状況の範囲の [[使用状況] ページ](hid-usages.md#usage-page)

-   値を含むレポートのレポート ID

-   [使用状況 ID](hid-usages.md#usage-id)または使用範囲

-   使用法が[別名で使用](hid-usages.md#aliased-usages)されるかどうかを示します

-   使用状況または使用状況の範囲を含む[リンクコレクション](link-collections.md)に関する情報

-   値のサイズ (ビット単位) とレポート数 (構造体によって記述される個別の値の数)

-   各値の属性 (null 値を含むかどうか、単位と指数、論理範囲と物理的な範囲など)

-   使用状況または使用状況の範囲に関連付けられている文字列記述子と指定子に関する情報

-   HID パーサーによって使用状況または使用状況の範囲が割り当てられる[データインデックス](data-indices.md)に関する情報

一般に、値機能配列で記述されているすべての使用について、次の条件が保持されます。

-   各機能構造は、使用状況、使用範囲、または変数のメイン項目に関連付けられている[使用状況の値の配列](#usage-value-array)を表します。 配列のメイン項目は、値に対してサポートされていません。

-   エイリアス化された使用法を使用できます。 使用範囲のエイリアスを指定することはできません。 エイリアス化された値は、ボタン機能配列にリンクされているエイリアスボタンと同じように、値機能配列内で一緒にリンクされます。 「[変数のメイン項目でのボタンの使用](button-capability-arrays.md#button-usages-in-a-variable-main-item)方法」を参照してください。

-   HID パーサーでは、必要最小限の使用法のみを使用して、各値に使用法を割り当てます。 パーサーは、使用法をレポート記述子で指定されている順序で割り当てます。 不要なレポート記述子での使用は破棄されます。 値機能配列に、破棄された使用法に関する情報が含まれていません。

-   HID パーサーは、機能配列に記述されている各使用方法に一意の[データインデックス](data-indices.md)を割り当てます。

データインデックスが値にどのように割り当てられるかについては、「[データインデックス](data-indices.md)」を参照してください。

### <a href="" id="usage-value-array"></a>使用状況の値の配列

*使用状況の値の配列*は、メイン項目に指定されている一連の連続する値であり、そのすべてに同じ使用法が割り当てられています。 これは、レポート数が1より大きいメインアイテムに対して1つの使用法のみが指定されている場合に発生します。

次の図は、5つのデータ項目 (各6ビット) を含む使用状況値配列の例を示しています。

![5つのデータ項目 (それぞれ6ビット) を含む使用状況値の配列を示す図](images/repcount.png)

前の例では、このような使用状況値配列の値機能構造では、 **Isrange**メンバーが**FALSE**に設定され、その**NotRange**メンバーが17に、 **reportcount**メンバーが5に設定され、 **bitsize**メンバーが6に設定されています。

使用状況のレポート数が1である場合は、 **Hidp\_Getusage value**を使用して使用状況の値を抽出します。 使用状況のレポートカウントが1より大きい場合、 **Hidp\_Getusage value**は使用状況の値の配列の最初のデータ項目のみを返します。 使用状況値配列内のすべてのデータ項目を抽出するには、 [**Hidp\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)を使用します。

 

 





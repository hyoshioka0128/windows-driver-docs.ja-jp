---
title: 機能の値の配列
description: 機能の値の配列
ms.assetid: d447dda6-a1e5-4e57-b06f-f79f8662c236
keywords:
- WDK を非表示機能の配列を値します。
- WDK の HID 配列
- コレクションの WDK を非表示の機能
- WDK の HID 使用法の値を配列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cc87ae12413ba4545251117fba3db7a832061d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538879"
---
# <a name="value-capability-arrays"></a>機能の値の配列





A*値機能配列*でサポートされている値の使用状況に関する情報を格納、[最上位のコレクション](top-level-collections.md)HID レポートの特定の種類。 コレクションの配列の機能に関する情報が含まれているその[ **HIDP\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)構造体。

ユーザー モード アプリケーションまたはカーネル モード ドライバーは、次のいずれかを使用して[HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)ボタンの機能情報を取得します。

-   [**HidP\_GetValueCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539754)呼び出し元が指定したレポートの種類に含まれているすべての値を表す値機能の配列を返します。

-   [**HidP\_GetSpecificValueCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539737)ことによって、呼び出し元が指定した使用状況] ページ、使用状況、リンクのコレクション、およびレポートの種類、返す値機能の情報をフィルターします。

値機能の配列に含まれる[ **HIDP\_値\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539832)構造体、うちそれぞれについて、次の情報を説明します、 [するHID使用法](hid-usages.md)または[使用範囲](hid-usages.md#usage-range):

-   [使用状況 ページ](hid-usages.md#usage-page)使用または使用状況の範囲

-   値を含むレポートのレポート ID

-   A[使用状況 ID](hid-usages.md#usage-id)または使用状況の範囲

-   使用方法は、かどうかを示す、[別名の使用状況](hid-usages.md#aliased-usages)

-   については、[リンク コレクション](link-collections.md)使用状況や使用状況の範囲を格納しています。

-   値、およびレポート数 (つまり、構造体で記述される個々 の値の数) のビット単位のサイズ

-   それぞれの値の属性を含む: null 値をそのユニットと指数部の論理的および物理的な範囲を持つかどうか

-   文字列記述子と使用状況や使用状況の範囲に関連付けられている指定子について

-   については、[データのインデックス](data-indices.md)HID パーサーを使用または使用状況の範囲を割り当てること

一般に、次の条件は、値機能の配列で説明されているすべての使用状況の保持します。

-   各機能の構造は、使用量、使用状況の範囲を表しますまたは[値配列の使用状況](#usage-value-array)変数の主な項目に関連付けられています。 値では、主な項目の配列はサポートされていません。

-   エイリアスの使用法を使用できます。 使用状況の範囲は、エイリアスにすることはできません。 エイリアス化された値が、ボタン機能の配列でリンクとしてエイリアス化ボタンと同じ方法で値機能の配列でまとめてリンクされます。 参照してください[変数の主な項目内の使用状況をボタン](button-capability-arrays.md#button-usages-in-a-variable-main-item)します。

-   HID パーサーでは、必要な最小の使用のみを使用して、各値に、使用量を割り当てます。 パーサーでは、使用状況レポート記述子で指定されている順序で割り当てられます。 必要でない使用状況のレポート記述子は破棄されます。 値の機能の配列では、破棄された使用状況に関する情報は含まれません。

-   HID パーサー割り当てます一意[データ インデックス](data-indices.md)機能配列で説明されている各使用法をします。

値にデータのインデックスを割り当てる方法については、次を参照してください。[データのインデックス](data-indices.md)します。

### <a href="" id="usage-value-array"></a> 使用状況の値の配列

A*値配列の使用状況*は連続する同じ使用量が割り当てられているすべてのメイン アイテムで指定された値のセットです。 これは、だけがレポートの数は 2 つ以上の主な項目の 1 つの使用量が指定した場合に発生します。

次の図は、5 つのデータ項目、各 6 つのビット長を格納する使用率値の配列の例を示します。

![各 6 ビット長、5 つのデータ項目を含む使用率値の配列を示す図](images/repcount.png)

使用法値配列、構造体の値の機能が、前の例では、その**IsRange**メンバーに設定**FALSE**その**NotRange.Usage** 17、設定メンバーその**ReportCount**メンバーが 5 に設定し、その**BitSize**メンバーが 6 に設定します。

使用状況レポートの数が 1 の場合を使用して、 **HidP\_GetUsageValue**使用法の値を抽出します。 使用状況のレポートの数が 1 より大きい場合**HidP\_GetUsageValue**使用状況の値の配列の最初のデータ項目のみが返されます。 使用状況の値の配列内のすべてのデータ項目を抽出するには使用[ **HidP\_GetUsageValueArray**](https://msdn.microsoft.com/library/windows/hardware/ff539750)します。

 

 





---
title: 子デバイスと制御メソッドを列挙する
description: 子デバイスと制御メソッドを列挙する
ms.assetid: fe0553df-a5b9-46c4-8e1d-8b89a7d4ad67
keywords:
- ACPI デバイス WDK、子デバイスの列挙
- ACPI デバイス WDK、列挙制御メソッド
- ACPI 名前空間 WDK
- ACPI 制御方法 WDK、列挙
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e9300f06b07c88f88f5c6ced9c2765c9ee1b8bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826124"
---
# <a name="enumerating-child-devices-and-control-methods"></a>子デバイスと制御メソッドを列挙する


デバイスである ACPI 名前空間 ("ABCD" という名前のデバイスなど) では、デバイスの子デバイスである子オブジェクトや、デバイスでサポートされている制御メソッドである子オブジェクトを持つことができます。 親デバイスの子デバイスである子オブジェクトは、子デバイスまたはコントロールメソッドである子オブジェクトを再帰的に持つことができます。 たとえば、次の簡略化された ACPI 名前空間では、ACPI 名前空間のルートは '\\' によって指定され、オブジェクト ' ABCD ' は ACPI 名前空間のルートの直下の子であるデバイスです。 さらに、デバイス ' ABCD ' には、' CHL1 ' と ' CHL2 ' という名前の直接の子デバイスが2つあります。また、'\_FOO ' という名前のコントロールメソッドである子オブジェクトもあります。 さらに、子デバイス ' CHL2 ' には ' CHL3 ' という名前の子デバイスがあり、デバイス "CHL3" には '\_FOO. ' という名前のコントロールメソッドである子オブジェクトがあります。

```syntax
\     root of ACPI namespace
 ABCD            parent device 
    CHL1         child device of ABCD
    CHL2         child device of ABCD
       CHL3      child device of CHL2
          _FOO   control method
 _FOO            control method
```

[**Ioctl\_acpi\_eval\_メソッド\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)または[**IOCTL\_acpi\_ASYNC\_eval\_メソッド\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex)を使用する場合、デバイスのドライバーによって、acpi 名前空間にコントロールメソッドのパスと名前が指定されます。 デバイスとデバイスの子オブジェクトのパスと名前を取得するために、Windows では、 [**IOCTL\_ACPI\_ENUM\_CHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求がサポートされています。 例として、このセクションで提供されている簡易 ACPI 名前空間を参照すると、デバイス ' ABCD ' のデバイススタック内のドライバーは、この要求を使用して次の操作を行うことができます。

-   ' Abcd ' のデバイス ' ABCD ' と直接の子デバイスを列挙します。 たとえば、要求を使用して '\\ABCD, ' '\\ABCD を返すことができます。CHL1、' および '\\ABCD です。CHL2.'

-   ' ABCD ' の名前空間にあるすべてのデバイスを再帰的に列挙します。 たとえば、要求を使用して '\\ABCD, ' '\\ABCD を返すことができます。CHL1, ' '\\ABCD.CHL2、' および '\\ABCD です。CHL2.CHL3.'

-   指定された名前の ' ABCD ' のすべての子孫子オブジェクトを再帰的に列挙します。 指定された名前は、同じ名前を持つ子オブジェクトだけが列挙されるように、フィルターとして機能します。 たとえば、指定された名前 '\_FOO, ' に対して、要求を使用して '\\ABCD を返すことができます。\_FOO ' と '\\ABCD.CHL2.CHL3.\_FOO. '

ドライバーは、コントロールメソッドのパスと名前を取得した後、「acpi[制御メソッドを同期的に評価](evaluating-acpi-control-methods-synchronously.md)する」で説明されているように、ACPI\_ASYNC\_\_EVAL\_METHOD\_メソッド\_ex または ioctl に\_\_入力としてパスと名前を指定できます。\_

[**IOCTL\_ACPI\_enum\_children**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求では、入力として、ドライバーによって割り当てられた可変長[**ACPI\_列挙型\_子\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_input_buffer)次のメンバーを含む入力\_バッファー構造を受け取ります。

<a href="" id="signature"></a>**折本**  
入力バッファーの署名。 ACPI\_列挙型\_子\_入力\_バッファー\_署名に設定する必要があります。

<a href="" id="flags"></a>**示す**  
ACPI ドライバーが列挙するデバイスの ACPI 名前空間内のオブジェクトを決定するフラグ。 ACPI ドライバーは、ACPI 名前空間のルートで始まる列挙されたオブジェクトの完全なパスと名前を返します。 フラグは、次のいずれかの値に設定する必要があります。

<a href="" id="enum-children-immediate-only"></a>子\_\_即時\_のみ列挙  
デバイスを列挙し、デバイスの直接の子デバイスを列挙します。

<a href="" id="enum-children-multilevel"></a>列挙型\_子\_複数レベル  
デバイスを列挙し、デバイスのすべての子デバイスを再帰的に列挙します。

<a href="" id="enum-children-multilevel----enum-children-name-is-filter-"></a>複数レベルの\_子\_列挙型 | |列挙型\_子\_名前\_は\_フィルターです   
子と列挙型\_子と列挙型のビットごとの OR\_\_名前\_は\_フィルターによって、名前が**name**メンバーによって指定されたものと同じであるデバイスの子オブジェクトが列挙されます。

<a href="" id="namelength"></a>**NameLength**  
**名前**配列に格納されている ASCII 文字の数。

<a href="" id="name"></a>**指定**  
NULL で終わる4文字の ASCII 配列。これは、ACPI ドライバーが子オブジェクトの列挙を同じ名前のオブジェクトに制限するために使用する子オブジェクトの名前を格納します。

IOCTL\_ACPI\_ENUM\_CHILDREN 要求は、ドライバーによって割り当てられた可変長\_ACPI の子オブジェクトのパスと名前を返します。これは、次のメンバーを含む\_\_出力\_バッファーに格納されます。

<a href="" id="signature"></a>**折本**  
出力バッファーの署名。 ACPI\_列挙型\_子に設定する必要があります。これは、\_出力\_バッファー\_署名に設定する必要があります。

<a href="" id="numberofchildren"></a>**NumberOfChildren**  
**子**配列の子\_列挙型\_子の要素の数。

<a href="" id="children"></a>**子供**  
ACPI\_列挙型\_子の要素の配列。 ACPI\_列挙型\_子構造体の**name**メンバーには、子オブジェクトのパスと名前が含まれます。 **Flags**メンバーは、子オブジェクトに子オブジェクトがあるかどうかを示します。

ドライバーによって割り当てられる出力バッファーが、列挙されたすべての子名を返すのに十分な大きさではない場合、ACPI ドライバーは子名を返しません。また、要求については、IO\_状態\_ブロックの**状態**メンバーを\_バッファー\_オーバーフローに設定します。 この場合、出力バッファーのサイズ (バイト単位) が少なくとも**sizeof**(acpi\_列挙型\_子\_出力\_バッファー\_署名) である場合、ACPI ドライバーは、要求されたパスと名前を取得するために必要なサイズ (バイト単位) に**numberofchildren**を設定します。

子デバイスを列挙する方法の詳細については、「 [IOCTL\_ACPI\_ENUM\_CHILDREN 要求](sending-an-ioctl-acpi-enum-children-request.md)」を参照してください。

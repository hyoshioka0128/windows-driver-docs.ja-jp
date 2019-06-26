---
title: 子デバイスと制御メソッドを列挙する
description: 子デバイスと制御メソッドを列挙する
ms.assetid: fe0553df-a5b9-46c4-8e1d-8b89a7d4ad67
keywords:
- ACPI デバイス WDK、列挙子のデバイス
- ACPI デバイス WDK、コントロールのメソッドを列挙します。
- WDK の ACPI 名前空間
- ACPI の制御方法、WDK を列挙します。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 13e053c5a360d38fd08e03749d361a0696bf1698
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355847"
---
# <a name="enumerating-child-devices-and-control-methods"></a>子デバイスと制御メソッドを列挙する


たとえば、デバイスであるオブジェクト 'ABCD'--という名前のデバイス ACPI 名前空間では、子オブジェクトは、デバイスの子デバイスまたはデバイスでサポートされているコントロールのメソッドであることができます。 親デバイスの子デバイスは、任意の子オブジェクトはさらに、再帰的にある子デバイスである子オブジェクトやメソッドを制御します。 たとえば、次の簡略化の ACPI 名前空間で ACPI 名前空間のルートで指定された '\\' オブジェクト 'ABCD' がデバイスを ACPI 名前空間のルートの直下の子であるとします。 さらに、デバイス 'ABCD' が 'CHL1' という名前の 2 つの直接の子デバイスと 'CHL2' と、子オブジェクトという名前の制御メソッドは '\_FOO '。 さらに、子デバイス 'CHL2' が 'CHL3' という名前の子デバイスとデバイス"CHL3"という名前のコントロール メソッドである子オブジェクトがあります '\_FOO '。

```syntax
\     root of ACPI namespace
 ABCD            parent device 
    CHL1         child device of ABCD
    CHL2         child device of ABCD
       CHL3      child device of CHL2
          _FOO   control method
 _FOO            control method
```

使用する[ **IOCTL\_ACPI\_EVAL\_メソッド\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)または[ **IOCTL\_ACPI\_ASYNC\_EVAL\_メソッド\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex)デバイスのドライバーを ACPI 名前空間管理メソッドの名前とパスを提供します。 デバイスのデバイスと子オブジェクトの名前とパスを取得するには、Windows のサポート、 [ **IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求。 例として、デバイスのデバイス スタック内のドライバーこのセクションで説明する簡略化された ACPI 名前空間を参照する 'ABCD' は、次の操作をこの要求を使用できます。

-   デバイス 'ABCD' と 'ABCD ' の直接の子デバイスを列挙します。 要求を使用して、返されるなど '\\ABCD、''\\ABCD します。CHL1、' と '\\ABCD します。CHL2 '。

-   再帰的に 'ABCD ' の名前空間のすべてのデバイスを列挙します。 要求を使用して、返されるなど '\\ABCD、''\\ABCD します。CHL1、' '\\ABCD します。CHL2、' と '\\ABCD します。CHL2 します。CHL3 '。

-   再帰的には、指定された名前の 'ABCD' のすべての子オブジェクトを列挙します。 指定された名前は、同じ名前を持つ子オブジェクトのみを列挙するために、フィルターとして機能します。 たとえば、指定された名前 '\_FOO' を返す要求を使用できる'\\ABCD\_ 。FOO' と '\\ABCD します。CHL2 します。CHL3 します。\_FOO '。

ドライバーは、コントロールのメソッドの名前とパスを取得した後、その IOCTL への入力として名前とパスを指定できます\_ACPI\_EVAL\_メソッド\_EX または IOCTL\_ACPI\_ASYNC\_EVAL\_メソッド\_」の説明に従って、EX [ACPI コントロールのメソッドを同期的評価](evaluating-acpi-control-methods-synchronously.md)します。

[ **IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)ドライバーに割り当てられた可変長を入力としての要求の受け取り[ **ACPI\_列挙型\_子\_入力\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_input_buffer)次のメンバーを含む構造体。

<a href="" id="signature"></a>**署名**  
入力のバッファーは、ACPI に設定する必要がありますが、署名\_ENUM\_子\_入力\_バッファー\_署名します。

<a href="" id="flags"></a>**フラグ**  
ACPI のドライバーを列挙するデバイスの ACPI 名前空間内のオブジェクトを決定するフラグ。 ACPI ドライバーでは、ACPI 名前空間のルートを持つ列挙型のオブジェクトの先頭の名前と完全なパスを返します。 次の値のいずれかに、フラグを設定する必要があります。

<a href="" id="enum-children-immediate-only"></a>列挙型\_子\_イミディ エイト\_のみ  
デバイスを列挙し、デバイスの直接の子デバイスを列挙します。

<a href="" id="enum-children-multilevel"></a>列挙型\_子\_マルチレベル  
デバイスを列挙し、再帰的には、デバイスのすべての子デバイスを列挙します。

<a href="" id="enum-children-multilevel----enum-children-name-is-filter-"></a>ENUM\_CHILDREN\_MULTILEVEL || ENUM\_CHILDREN\_NAME\_IS\_FILTER   
ビットごとまたはの列挙型\_子および列挙型\_子\_名前\_IS\_フィルターは、名前を持つ、によって指定されたのと同じデバイスの子オブジェクトを列挙します、**名前**。メンバー。

<a href="" id="namelength"></a>**NameLength**  
文字の ASCII の数、**名前**配列が含まれています。

<a href="" id="name"></a>**名**  
NULL で終わる 4 文字 ASCII 格納する配列の ACPI ドライバーを使用して、同じ名前を持つこれらのオブジェクトへの子オブジェクトの列挙体を制限する子オブジェクトの名前。

IOCTL\_ACPI\_ENUM\_子要求はドライバーによって割り当てられたの可変長 ACPI の子オブジェクトの名前とパスを返します\_ENUM\_子\_出力\_、次のメンバーを格納しているバッファー。

<a href="" id="signature"></a>**署名**  
ACPI に設定する必要があります出力バッファーの署名\_ENUM\_子\_出力\_バッファー\_署名します。

<a href="" id="numberofchildren"></a>**NumberOfChildren**  
ACPI の型の要素の数\_ENUM\_内の子、**子**配列。

<a href="" id="children"></a>**子**  
ACPI の型の要素の配列\_ENUM\_子。 **名前**ACPI のメンバー\_ENUM\_子構造体には、子オブジェクトの名前とパスが含まれています、**フラグ**メンバーは、子オブジェクトに子があるかどうかを示しますオブジェクト。

ACPI ドライバーでは、名前とセットに、なしの子が返されます、ドライバーによって割り当てられる出力バッファー、すべての列挙子の名前を取得するのに十分な大きさでない場合、**状態**、IO のメンバー\_状態\_のブロック、要求の状態を\_バッファー\_オーバーフローが発生します。 この場合、出力バッファーのバイト単位のサイズは少なくとも**sizeof**(ACPI\_ENUM\_子\_出力\_バッファー\_署名)、ACPI ドライバーも設定**コード**要求されたパスと名前の取得に必要なサイズ (バイト単位)。

子デバイスを列挙する方法の詳細については、次を参照してください。[送信 IOCTL\_ACPI\_ENUM\_子要求](sending-an-ioctl-acpi-enum-children-request.md)。

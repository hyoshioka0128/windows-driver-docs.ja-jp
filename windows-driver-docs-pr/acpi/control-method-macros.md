---
title: 制御メソッドのマクロ
description: 制御メソッドのマクロ
ms.assetid: cffcfb7a-c949-4bc9-a92f-349f5637ab84
keywords:
- ACPI 制御方法 WDK、マクロ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 052e45c47d3af60e1e7fc9737bec3c3a65c60638
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824716"
---
# <a name="control-method-macros"></a>制御メソッドのマクロ


ドライバーは、次のマクロを使用して、[制御メソッドを評価](evaluating-acpi-control-methods.md)する ACPI ioctl で使用される入力引数を設定できます。

[**ACPI\_メソッド\_設定\_引数\_整数**](acpi-method-set-argument-integer.md)

[**ACPI\_メソッド\_設定\_引数\_文字列**](acpi-method-set-argument-string.md)

[**ACPI\_メソッド\_設定\_引数\_バッファー**](acpi-method-set-argument-buffer.md)

制御メソッドを評価する ACPI Ioctl は、 [**acpi\_\_\_EVAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)の**引数**メンバーに出力引数を返します。この場合、**引数**メンバーは[**acpi\_メソッドの配列です。\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)の構造体。 ドライバーは、次のマクロを使用して、引数構造\_の ACPI\_メソッドの配列を処理できます。

[**ACPI\_メソッド\_引数\_の長さ**](acpi-method-argument-length.md)

[**ACPI\_メソッド\_引数\_\_引数からの長さ\_** ](acpi-method-argument-length-from-argument.md)

[**ACPI\_メソッド\_次の\_引数**](acpi-method-next-argument.md)

[**IOCTL\_ACPI\_ENUM\_CHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求は、要求が送信されるデバイスの名前空間にある子オブジェクトのパスと名前を取得します。 ACPI ドライバーは、ACPI 名前空間のルートで始まる列挙されたオブジェクトの完全なパスと名前を返します。 子オブジェクトのパスと名前は、 [**acpi\_列挙型\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer) **子の子メンバーに**返されます。**この場合、子メンバーは**、 [**acpi\_列挙型の配列です。_t_11_ 子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)構造体。 ドライバーは、次のマクロを使用して、ACPI\_列挙型\_子構造体の配列を処理することができます。

[**ACPI\_列挙\_子\_次へ**](acpi-enum-child-next.md)

[**ACPI\_列挙型\_子\_\_子からの\_の長さ**](acpi-enum-child-length-from-child.md)

 

 





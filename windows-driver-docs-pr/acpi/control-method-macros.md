---
title: 制御メソッドのマクロ
description: 制御メソッドのマクロ
ms.assetid: cffcfb7a-c949-4bc9-a92f-349f5637ab84
keywords:
- ACPI 制御メソッド WDK、マクロ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b240e0e0a329502d1695950221999adbab4aa19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355857"
---
# <a name="control-method-macros"></a>制御メソッドのマクロ


ドライバーは次のマクロを使用して、ACPI Ioctl で使用される入力引数を設定する[制御メソッドを評価](evaluating-acpi-control-methods.md):

[**ACPI\_メソッド\_設定\_引数\_整数**](acpi-method-set-argument-integer.md)

[**ACPI\_メソッド\_設定\_引数\_文字列**](acpi-method-set-argument-string.md)

[**ACPI\_メソッド\_設定\_引数\_バッファー**](acpi-method-set-argument-buffer.md)

コントロールのメソッド戻り値の出力引数を評価する ACPI Ioctl、**引数**のメンバー、 [ **ACPI\_EVAL\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)構造、場所、**引数**メンバーの配列は、 [ **ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)構造体。 ドライバーは、次のマクロを使用して ACPI の配列を処理する\_メソッド\_引数構造体。

[**ACPI\_メソッド\_引数\_長さ**](acpi-method-argument-length.md)

[**ACPI\_メソッド\_引数\_長さ\_FROM\_引数**](acpi-method-argument-length-from-argument.md)

[**ACPI\_メソッド\_次\_引数**](acpi-method-next-argument.md)

[ **IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求は、要求を送信するデバイスの名前空間内の子オブジェクトの名前とパスを取得します。 ACPI ドライバーでは、ACPI 名前空間のルートを持つ列挙型のオブジェクトの先頭の名前と完全なパスを返します。 子オブジェクトの名前とパスが返されます、**子**のメンバー、 [ **ACPI\_ENUM\_子\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)構造、場所、**子**メンバーの配列は、 [ **ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)構造体. ドライバーは、次のマクロを使用して ACPI の配列を処理する\_ENUM\_子構造体。

[**ACPI\_ENUM\_子\_[次へ]** ](acpi-enum-child-next.md)

[**ACPI\_ENUM\_CHILD\_LENGTH\_FROM\_CHILD**](acpi-enum-child-length-from-child.md)

 

 





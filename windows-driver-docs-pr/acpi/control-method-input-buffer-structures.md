---
title: 制御メソッドの入力バッファーの構造
description: 制御メソッドの入力バッファーの構造
ms.assetid: 41d4c53f-9dc7-4723-9707-ae48ff07f5f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a75c4386096b2bf34dd048e3c9322345912a608
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824272"
---
# <a name="control-method-input-buffer-structures"></a>制御メソッドの入力バッファーの構造


ACPI ドライバーでは、 [**IOCTL\_acpi\_EVAL\_METHOD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)要求がサポートされています。 デバイスのドライバーは、この要求を使用して、要求が送信されるデバイスの ACPI 名前空間の直下の子オブジェクトである制御メソッドを評価できます。 IOCTL\_ACPI\_EVAL\_METHOD 要求では、次の入力構造がサポートされています。

<a href="" id="acpi-eval-input-buffer"></a>[**ACPI\_EVAL\_入力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)  
この構造体は、バッファーのシグネチャと、入力引数を受け取らないコントロールメソッドの名前を提供します。

<a href="" id="acpi-eval-input-buffer-simple-integer"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純\_整数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)  
この構造体は、構造体のシグネチャ、コントロールメソッドの名前、および ULONG 型の単一の入力引数値を提供します。

<a href="" id="acpi-eval-input-buffer-simple-string"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)  
この構造体は、構造体のシグネチャ、コントロールメソッドの名前、および NULL で終わる ASCII 文字列である入力引数を提供します。

<a href="" id="acpi-eval-input-buffer-complex"></a>[**ACPI\_EVAL\_入力\_バッファー\_複雑**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)  
この構造体は、構造体のシグネチャ、コントロールメソッドの名前、および[**ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)構造体の入力配列を提供します。 配列には、このような構造体の7つの最大数を含めることができます。 ACPI\_メソッド\_引数の構造体には、ULONG 整数、ASCII 文字列、ACPI パッケージの説明、またはカスタムデータの配列を含めることができます。

また、Windows では、\_EX 要求である[**IOCTL\_ACPI\_EVAL\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)もサポートしています。 デバイスのドライバーは、この要求を使用して、要求が送信されるデバイスの ACPI 名前空間にある子孫の子オブジェクトである制御メソッドを評価できます。 IOCTL\_ACPI\_EVAL\_メソッド\_EX 要求では、次の入力構造がサポートされています。

<a href="" id="acpi-eval-input-buffer-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)  
この構造体は、構造体のシグネチャ、および入力引数を受け取らないコントロールメソッドのパスと名前を提供します。

<a href="" id="acpi-eval-input-buffer-simple-integer-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純な\_整数\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1_ex)  
この構造体は、構造体のシグネチャと、入力引数として ULONG64 型の単一の整数を受け取るコントロールメソッドのパスと名前を提供します。

<a href="" id="acpi-eval-input-buffer-simple-string-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_単純\_文字列\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)  
この構造体は、構造体のシグネチャと、1つの NULL で終わる ASCII 文字列を入力引数として受け取るコントロールメソッドのパスと名前を提供します。

<a href="" id="acpi-eval-input-buffer-complex-ex"></a>[**ACPI\_EVAL\_入力\_バッファー\_複雑な\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)  
この構造体は、構造体のシグネチャと、ACPI\_メソッド\_引数構造体を入力として受け取るコントロールメソッドのパスと名前を提供します。 配列には、このような構造体の7つの最大数を含めることができます。 ACPI\_メソッド\_引数の構造体には、ULONG 整数、ASCII 文字列、ACPI パッケージの説明、またはカスタムデータの配列を含めることができます。

デバイスの ACPI 名前空間の子オブジェクトのパスと名前を取得するために、デバイスのドライバーは、「[子デバイスの列挙と制御メソッド](enumerating-child-devices-and-control-methods.md)」で説明されているように、 [**IOCTL\_acpi\_ENUM\_CHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求を使用できます。

---
title: ACPI_METHOD_SET_ARGUMENT_INTEGER マクロ
description: ACPI_METHOD_SET_ARGUMENT_INTEGER マクロは、1つの整数値に対して ACPI_METHOD_ARGUMENT 構造体のメンバーを設定します。
ms.assetid: a79f9149-0ffe-483f-a45e-427b05ff0a11
keywords:
- ACPI_METHOD_SET_ARGUMENT_INTEGER マクロ ACPI デバイス
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7107b1678c4f5da1e27fc8af69ed95b06b22ef76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824060"
---
# <a name="acpi_method_set_argument_integer-macro"></a>ACPI\_メソッド\_設定\_引数\_整数マクロ


ACPI\_メソッド\_設定\_引数\_整数マクロは、1つの整数値に対して、 [**acpi\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)のメンバーを引数構造\_設定します。

<a name="syntax"></a>構文
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_INTEGER(
    MethodArgument,
    IntData
);
```

<a name="parameters"></a>パラメーター
----------

*Methodargument*   
引数構造\_の ACPI\_メソッドへのポインター。

*Intdata*   
ULONG 型の整数値。

<a name="return-value"></a>戻り値
------------

このマクロは値を返しません。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して、ULONG 型の単一の整数値を指定する\_引数の構造体を、ACPI\_メソッドのメンバーに設定できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
<tr>
<td><p>Header</p></td>
<td>Acpiioct (Acpiioct を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 

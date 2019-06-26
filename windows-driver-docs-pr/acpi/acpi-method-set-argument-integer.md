---
title: ACPI_METHOD_SET_ARGUMENT_INTEGER マクロ
description: ACPI_METHOD_SET_ARGUMENT_INTEGER マクロは、1 つの整数値の ACPI_METHOD_ARGUMENT 構造体のメンバーを設定します。
ms.assetid: a79f9149-0ffe-483f-a45e-427b05ff0a11
keywords:
- ACPI_METHOD_SET_ARGUMENT_INTEGER マクロ ACPI デバイス
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 92b2b0cdfd3d390e4121f0610d62d27d07615fb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355867"
---
# <a name="acpimethodsetargumentinteger-macro"></a>ACPI\_メソッド\_設定\_引数\_整数マクロ


ACPI\_メソッド\_設定\_引数\_整数マクロがのメンバーを設定、 [ **ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)1 つの整数値の構造体。

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

*MethodArgument*   
ACPI へのポインター\_メソッド\_引数構造体。

*IntData*   
ULONG 型の整数値。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して ACPI のメンバーを設定する\_メソッド\_ULONG 型の 1 つの整数値を提供する引数の構造体。

<a name="requirements"></a>必要条件
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
<td>Acpiioct.h (Acpiioct.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 

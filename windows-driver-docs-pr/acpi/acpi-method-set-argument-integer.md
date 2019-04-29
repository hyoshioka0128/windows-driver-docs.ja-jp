---
title: ACPI_METHOD_SET_ARGUMENT_INTEGER マクロ
description: ACPI_METHOD_SET_ARGUMENT_INTEGER マクロは、1 つの整数値の ACPI_METHOD_ARGUMENT 構造体のメンバーを設定します。
ms.assetid: a79f9149-0ffe-483f-a45e-427b05ff0a11
keywords:
- ACPI_METHOD_SET_ARGUMENT_INTEGER マクロ ACPI デバイス
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 61fbedf536c27bd6374c8a422e66bb7d28a37c29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328846"
---
# <a name="acpimethodsetargumentinteger-macro"></a>ACPI\_メソッド\_設定\_引数\_整数マクロ


ACPI\_メソッド\_設定\_引数\_整数マクロがのメンバーを設定、 [ **ACPI\_メソッド\_引数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)1 つの整数値の構造体。

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


[**ACPI\_メソッド\_引数**](https://msdn.microsoft.com/library/windows/hardware/ff536125) 

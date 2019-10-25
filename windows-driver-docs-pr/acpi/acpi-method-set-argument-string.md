---
title: ACPI_METHOD_SET_ARGUMENT_STRING マクロ
description: ACPI_METHOD_SET_ARGUMENT_STRING マクロは、文字列値の ACPI_METHOD_ARGUMENT 構造体のメンバーを設定します。
ms.assetid: e0c037a9-65b6-4d6a-9ed6-d9296c14df07
keywords:
- ACPI_METHOD_SET_ARGUMENT_STRING マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e5d6746ee931adde6a75860a2fe1eea0e7f3194
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824055"
---
# <a name="acpi_method_set_argument_string-macro"></a>ACPI\_メソッド\_設定\_引数\_文字列マクロ


ACPI\_メソッド\_設定\_引数\_STRING マクロは、文字列値に対して、 [**acpi\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)のメンバーを引数構造\_設定します。

<a name="syntax"></a>構文
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_STRING(
    Argument,
    StrData
);
```

<a name="parameters"></a>パラメーター
----------

*引数*   
引数構造\_の ACPI\_メソッドへのポインター。

*Strdata*   
NULL で終わる ASCII 文字列へのポインター。

<a name="return-value"></a>戻り値
------------

このマクロは値を返しません。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して、NULL で終わる ASCII 文字列を提供する、引数の構造\_、ACPI\_メソッドのメンバーを設定できます。

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

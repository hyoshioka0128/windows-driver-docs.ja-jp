---
title: ACPI_METHOD_NEXT_ARGUMENT マクロ
description: ACPI_METHOD_NEXT_ARGUMENT 構造体は ACPI_METHOD_ARGUMENT 構造体の配列内の次の ACPI_METHOD_ARGUMENT 構造体へのポインターを返します。
ms.assetid: c723b11b-1657-4a78-a6a1-26bd916604a4
keywords:
- ACPI_METHOD_NEXT_ARGUMENT マクロ ACPI デバイス
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 47c41af603a78680f38c1da856d3e4e7a5c2fb6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824064"
---
# <a name="acpi_method_next_argument-macro"></a>ACPI\_メソッド\_NEXT\_ARGUMENT マクロ


ACPI\_メソッド\_次の\_引数構造体は、次の[**acpi\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)へのポインターを返します。このメソッドは、ACPI\_メソッド\_引数構造体の配列にあります。\_

<a name="syntax"></a>構文
------

```cpp
 ACPI_METHOD_NEXT_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>パラメーター
----------

*引数*   
Acpi\_メソッド\_引数構造体の配列にある、ACPI\_メソッドへのポインター\_引数構造体。

<a name="return-value"></a>戻り値
------------

次の ACPI\_メソッドへのポインター\_、ACPI\_メソッドの配列内の引数構造体\_引数構造体。

<a name="remarks"></a>注釈
-------

このような構造体の配列で、ACPI\_メソッドへのポインター\_引数構造体を指定すると、ドライバーはこのマクロを使用して、配列内の次の構造体 (存在する場合) へのポインターを計算できます。

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

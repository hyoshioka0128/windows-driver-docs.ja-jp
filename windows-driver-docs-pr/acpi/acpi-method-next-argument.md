---
title: ACPI_METHOD_NEXT_ARGUMENT マクロ
description: ACPI_METHOD_NEXT_ARGUMENT 構造体は、ACPI_METHOD_ARGUMENT 構造体の配列で、[次へ] の ACPI_METHOD_ARGUMENT 構造体へのポインターを返します。
ms.assetid: c723b11b-1657-4a78-a6a1-26bd916604a4
keywords:
- ACPI_METHOD_NEXT_ARGUMENT マクロ ACPI デバイス
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 596761fcbc027d1d7f3da5c23ed3b5f2ba3b05f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355880"
---
# <a name="acpimethodnextargument-macro"></a>ACPI\_メソッド\_次\_引数マクロ


ACPI\_メソッド\_次\_引数構造体へのポインターを返します[ **ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)構造体配列の ACPI\_メソッド\_引数構造体。

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
ACPI へのポインター\_メソッド\_ACPI の配列の構造体を引数\_メソッド\_引数構造体。

<a name="return-value"></a>戻り値
------------

[次へ] の ACPI へのポインター\_メソッド\_ACPI の配列の構造体を引数\_メソッド\_引数構造体。

<a name="remarks"></a>注釈
-------

ACPI にポインターを与えられた\_メソッド\_引数構造、このような構造体の配列で、ドライバーを使用してこのマクロ、配列内の次の構造体へのポインターの計算が存在する場合。

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

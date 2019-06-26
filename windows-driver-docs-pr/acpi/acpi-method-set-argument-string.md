---
title: ACPI_METHOD_SET_ARGUMENT_STRING macro
description: ACPI_METHOD_SET_ARGUMENT_STRING マクロは、文字列値に対して ACPI_METHOD_ARGUMENT 構造体のメンバーを設定します。
ms.assetid: e0c037a9-65b6-4d6a-9ed6-d9296c14df07
keywords:
- ACPI_METHOD_SET_ARGUMENT_STRING マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38e1af1b8530d391432ad2a8c94a6807a6685918
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355861"
---
# <a name="acpimethodsetargumentstring-macro"></a>ACPI\_メソッド\_設定\_引数\_文字列マクロ


ACPI\_メソッド\_設定\_引数\_文字列マクロがのメンバーを設定、 [ **ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)文字列値の構造体。

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
ACPI へのポインター\_メソッド\_引数構造体。

*StrData*   
NULL で終わる ASCII 文字列へのポインター。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して ACPI のメンバーを設定する\_メソッド\_が NULL で終わる ASCII 文字列を指定する引数の構造体。

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
<td>Acpiioct.h (Acpiioct.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 

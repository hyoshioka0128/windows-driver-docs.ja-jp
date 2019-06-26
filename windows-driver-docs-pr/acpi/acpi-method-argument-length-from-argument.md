---
title: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロ
description: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロは、ACPI_METHOD_ARGUMENT 構造体のデータ配列に含まれるデータのバイト単位のサイズを計算します。
ms.assetid: 46fe0382-1496-49eb-988d-2007885d2210
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb2c0c331d10f6b99661db36e477a471ab7444d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355884"
---
# <a name="acpimethodargumentlengthfromargument-macro"></a>ACPI\_メソッド\_引数\_長さ\_FROM\_引数マクロ


ACPI\_メソッド\_引数\_長さ\_FROM\_マクロの引数のデータ配列に含まれるデータのバイト単位のサイズを計算する、 [ **ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)構造体。

<a name="syntax"></a>構文
------

```cpp
void ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT(
    Argument
);
```

<a name="parameters"></a>パラメーター
----------

*引数*   
ACPI へのポインター\_メソッド\_引数構造体。

<a name="return-value"></a>戻り値
------------

含まれているデータのバイト単位のサイズ、**データ**配列の ACPI\_メソッド\_引数が構造体を*引数*を指します。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して、内のデータのバイト単位のサイズを決定、**データ**配列の ACPI\_メソッド\_引数構造体。

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

 

 





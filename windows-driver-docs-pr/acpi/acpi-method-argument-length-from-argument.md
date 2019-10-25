---
title: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロ
description: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロは、ACPI_METHOD_ARGUMENT 構造体のデータ配列に格納されているデータのサイズをバイト単位で計算します。
ms.assetid: 46fe0382-1496-49eb-988d-2007885d2210
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bcd86f5d9679552f2f8c7db47ac69292227201
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824070"
---
# <a name="acpi_method_argument_length_from_argument-macro"></a>ACPI\_メソッド\_引数\_\_引数マクロからの長さ\_


ACPI\_メソッド\_引数\_\_引数マクロからの長さ\_は、 [**acpi\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)のデータ配列に格納されているデータのサイズ (バイト単位) を計算します。

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
引数構造\_の ACPI\_メソッドへのポインター。

<a name="return-value"></a>戻り値
------------

*引数*が指す引数構造\_、ACPI\_メソッドの**データ**配列に格納されているデータのサイズ (バイト単位)。

<a name="remarks"></a>注釈
-------

ドライバーはこのマクロを使用して、ACPI\_メソッド\_引数の構造体の**データ**配列内のデータのサイズ (バイト単位) を決定できます。

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

 

 





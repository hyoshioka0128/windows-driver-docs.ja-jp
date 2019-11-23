---
title: ACPI_METHOD_ARGUMENT_LENGTH マクロ
description: ACPI_METHOD_ARGUMENT_LENGTH マクロは、指定されたサイズのデータを格納する可変長 ACPI_METHOD_ARGUMENT 構造体のバイト単位のサイズをバイト単位で計算します。
ms.assetid: 8329c2eb-a787-4590-8de9-95078bbb85da
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c12ba630f51ae906db73937c91da531c00fddfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824066"
---
# <a name="acpi_method_argument_length-macro"></a>ACPI\_メソッド\_引数\_LENGTH マクロ


ACPI\_メソッド\_引数\_LENGTH マクロは、指定されたサイズ (バイト単位) のデータを含む可変長の[**ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)の構造体のサイズをバイト単位で計算します。

<a name="syntax"></a>構文
------

```cpp
void ACPI_METHOD_ARGUMENT_LENGTH(
    DataLength
);
```

<a name="parameters"></a>パラメーター
----------

*DataLength*   
ACPI\_メソッドの**データ**配列内のデータのサイズ (バイト単位)\_引数の構造体。

<a name="return-value"></a>戻り値
------------

可変長 ACPI\_メソッド\_引数の構造体のサイズ (バイト単位) は、サイズが*DataLength*である**データ**配列を含むことができます。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して、指定されたサイズの**データ**配列 (バイト単位) を含むことができる可変長の ACPI\_メソッド\_引数の構造体の必要なサイズをバイト単位で計算できます。

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

 

 





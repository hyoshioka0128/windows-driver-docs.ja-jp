---
title: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロ
description: ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロは、ACPI_METHOD_ARGUMENT 構造体のデータ配列に含まれるデータのバイト単位のサイズを計算します。
ms.assetid: 46fe0382-1496-49eb-988d-2007885d2210
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH_FROM_ARGUMENT マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d86579c407b4219c0e8ca4ac89d2bdfdb4e2589f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328870"
---
# <a name="acpimethodargumentlengthfromargument-macro"></a>ACPI\_メソッド\_引数\_長さ\_FROM\_引数マクロ


ACPI\_メソッド\_引数\_長さ\_FROM\_マクロの引数のデータ配列に含まれるデータのバイト単位のサイズを計算する、 [ **ACPI\_メソッド\_引数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)構造体。

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


[**ACPI\_メソッド\_引数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)

 

 





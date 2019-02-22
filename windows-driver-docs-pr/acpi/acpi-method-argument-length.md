---
title: ACPI_METHOD_ARGUMENT_LENGTH マクロ
description: ACPI_METHOD_ARGUMENT_LENGTH マクロでは、サイズをバイト単位で指定されたサイズのデータを含む可変長 ACPI_METHOD_ARGUMENT 構造体のバイト単位で計算されます。
ms.assetid: 8329c2eb-a787-4590-8de9-95078bbb85da
keywords:
- ACPI_METHOD_ARGUMENT_LENGTH マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5081f9204e5cf13ea97fa9916484d633654a641e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559092"
---
# <a name="acpimethodargumentlength-macro"></a>ACPI\_メソッド\_引数\_長さマクロ


ACPI\_メソッド\_引数\_長さマクロには、可変長のバイト単位で、サイズが計算されます[ **ACPI\_メソッド\_引数**。](https://msdn.microsoft.com/library/windows/hardware/ff536125) (バイト単位) の指定したサイズのデータを含む構造体。

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
内のデータのバイト単位で、サイズ、**データ**配列の ACPI\_メソッド\_引数構造体。

<a name="return-value"></a>戻り値
------------

可変長 ACPI のバイト単位のサイズ、\_メソッド\_引数構造体を含むことができます、**データ**(バイト単位)、サイズが配列*DataLength*します。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して、可変長 ACPI のバイト単位で、必要なサイズを計算する\_メソッド\_引数構造体を含めることができます、**データ**(バイト単位) の指定したサイズの配列。

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

 

 





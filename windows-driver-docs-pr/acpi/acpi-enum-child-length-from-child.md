---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロ
description: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロは、可変長 ACPI_ENUM_CHILD 構造体のサイズをバイト単位で計算します。
ms.assetid: 62be7cb5-4b71-4b8e-bad5-807623cd812a
keywords:
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 365671f8c38d1ca707a4dd58b4196d5c72b8f302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824127"
---
# <a name="acpi_enum_child_length_from_child-macro"></a>ACPI\_列挙型\_子\_\_子マクロからの長さ\_


ACPI\_ENUM\_子\_の子マクロからの長さ\_は、可変長の[**ACPI\_列挙型\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)構造体のサイズをバイト単位で計算します。

<a name="syntax"></a>構文
------

```cpp
void ACPI_ENUM_CHILD_LENGTH_FROM_CHILD(
    Child
);
```

<a name="parameters"></a>パラメーター
----------

*子*   
構造体のサイズをバイト単位で計算するための、ACPI\_列挙型の構造体へのポインター。子\_。

<a name="return-value"></a>戻り値
------------

*子*が指す子構造\_ACPI\_列挙型のバイト単位のサイズ。

<a name="remarks"></a>注釈
-------

ドライバーはこのマクロを使用し\_て、acpi\_列挙型の\_子構造体のサイズ (バイト単位) を計算します。この値は、 [**acpi 列挙型\_子であり、出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)構造体に\_ます。

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


[**ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)

[**ACPI\_列挙\_子\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)

 

 





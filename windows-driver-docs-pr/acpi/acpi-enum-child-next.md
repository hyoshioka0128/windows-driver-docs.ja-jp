---
title: ACPI_ENUM_CHILD_NEXT マクロ
description: ACPI_ENUM_CHILD_NEXT マクロは、可変長 ACPI_ENUM_CHILD 構造体の配列内の次の ACPI_ENUM_CHILD 構造体へのポインターを計算します。
ms.assetid: 1ff37770-b0ea-4275-9568-611ec125a0b6
keywords:
- ACPI_ENUM_CHILD_NEXT マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0082e2a8ec9ca30d6aeed8e8725e15b12bef5b87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824114"
---
# <a name="acpi_enum_child_next-macro"></a>ACPI\_列挙\_子\_次のマクロ


ACPI\_ENUM\_CHILD\_NEXT マクロは、次の[**acpi\_列挙型\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)構造体へのポインターを計算します。これは、変数の長さが acpi\_列挙型\_子構造体の配列に含まれています。

<a name="syntax"></a>構文
------

```cpp
void ACPI_ENUM_CHILD_NEXT(
    Child
);
```

<a name="parameters"></a>パラメーター
----------

*子*   
ACPI\_列挙型の変数へのポインター\_子の場合は、固定されていないポインターを次の ACPI\_\_列挙型 ACPI の配列内の子構造体に返す、列挙型\_子構造体。

<a name="return-value"></a>戻り値
------------

次の ACPI\_列挙型の\_子構造体を指すポインターは、可変長 ACPI\_列挙型\_子構造体の配列にあります。

<a name="remarks"></a>注釈
-------

ドライバーが IOCTL を使用して[ **\_acpi\_enum\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)デバイス名の配列を取得するために、子\_子デバイス\_名の配列を取得することを要求\_[**出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)要求では、このマクロを使用して、出力バッファーに格納されている**子**配列内の可変長 ACPI\_列挙型\_子構造体へのポインターのシーケンスを決定できます。

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

[**IOCTL\_ACPI\_列挙型\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)

 

 





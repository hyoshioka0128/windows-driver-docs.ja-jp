---
title: ACPI_ENUM_CHILD_NEXT マクロ
description: ACPI_ENUM_CHILD_NEXT マクロは、可変長 ACPI_ENUM_CHILD 構造体の配列で、次の ACPI_ENUM_CHILD 構造体へのポインターを計算します。
ms.assetid: 1ff37770-b0ea-4275-9568-611ec125a0b6
keywords:
- ACPI_ENUM_CHILD_NEXT マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49af38a832a22bcb06c11e1f5b5986c06506a5ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355889"
---
# <a name="acpienumchildnext-macro"></a>ACPI\_ENUM\_子\_次のマクロ


ACPI\_列挙型\_子\_マクロ [次へ]、[次へ] へのポインターを計算する[ **ACPI\_列挙型\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)の配列の構造可変長 ACPI\_ENUM\_子構造体。

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
ACPI の型の変数へのポインター\_列挙型\_を次の ACPI に固定されていないポインターを返す子\_列挙\_ACPI の可変長の配列内の子構造\_ENUM\_子構造体。

<a name="return-value"></a>戻り値
------------

[次へ] の ACPI へのポインター\_ENUM\_ACPI の可変長の配列内の子構造\_列挙\_子構造体。

<a name="remarks"></a>注釈
-------

ドライバーを使用した後、 [ **IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)で子デバイス名の配列を取得する要求、 [ **ACPI\_ENUM\_子\_出力\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)要求と、ドライバーは、このマクロを使用して、可変長 ACPIへのポインターのシーケンスを決定するには\_列挙型\_内の子構造体、**子**出力バッファーを含む配列。

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


[**ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)

[**ACPI\_ENUM\_子\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)

[**IOCTL\_ACPI\_ENUM\_CHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)

 

 





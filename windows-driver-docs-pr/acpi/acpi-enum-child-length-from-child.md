---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロ
description: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロは、可変長 ACPI_ENUM_CHILD 構造体のバイト単位のサイズを計算します。
ms.assetid: 62be7cb5-4b71-4b8e-bad5-807623cd812a
keywords:
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c750fe8d6cbcce2c3e8d0b2cb347c143faefc38b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355899"
---
# <a name="acpienumchildlengthfromchild-macro"></a>ACPI\_ENUM\_子\_長さ\_FROM\_子マクロ


ACPI\_ENUM\_子\_長さ\_FROM\_子マクロには、可変長のバイト単位で、サイズが計算されます[ **ACPI\_ENUM\_。子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)構造体。

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
ACPI の種類の構造体へのポインター\_ENUM\_構造体のバイト単位のサイズを計算する対象の子。

<a name="return-value"></a>戻り値
------------

ACPI のバイト単位のサイズを\_ENUM\_子構造体*子*を指します。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して ACPI のバイト単位のサイズを計算する\_ENUM\_内の子構造体、 [ **ACPI\_ENUM\_子\_出力\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)構造体。

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

 

 





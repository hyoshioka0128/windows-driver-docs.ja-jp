---
title: ACPI_ENUM_CHILD_NEXT マクロ
description: ACPI_ENUM_CHILD_NEXT マクロは、可変長 ACPI_ENUM_CHILD 構造体の配列で、次の ACPI_ENUM_CHILD 構造体へのポインターを計算します。
ms.assetid: 1ff37770-b0ea-4275-9568-611ec125a0b6
keywords:
- ACPI_ENUM_CHILD_NEXT マクロ ACPI デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 933fded8f739ba47d4f00cd070f2415435d48967
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328856"
---
# <a name="acpienumchildnext-macro"></a>ACPI\_ENUM\_子\_次のマクロ


ACPI\_列挙型\_子\_マクロ [次へ]、[次へ] へのポインターを計算する[ **ACPI\_列挙型\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536109)の配列の構造可変長 ACPI\_ENUM\_子構造体。

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

ドライバーを使用した後、 [ **IOCTL\_ACPI\_ENUM\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536147)で子デバイス名の配列を取得する要求、 [ **ACPI\_ENUM\_子\_出力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff536112)要求と、ドライバーは、このマクロを使用して、可変長 ACPIへのポインターのシーケンスを決定するには\_列挙型\_内の子構造体、**子**出力バッファーを含む配列。

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


[**ACPI\_ENUM\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536109)

[**ACPI\_ENUM\_子\_出力\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff536112)

[**IOCTL\_ACPI\_ENUM\_CHILDREN**](https://msdn.microsoft.com/library/windows/hardware/ff536147)

 

 





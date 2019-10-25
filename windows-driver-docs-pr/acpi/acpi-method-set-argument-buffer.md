---
title: ACPI_METHOD_SET_ARGUMENT_BUFFER マクロ
description: ACPI_METHOD_SET_ARGUMENT_BUFFER マクロは、データバッファーに指定されているカスタムデータの ACPI_METHOD_ARGUMENT 構造体のメンバーを設定します。
ms.assetid: 1f335814-fa9f-45c6-b970-10884e971ec1
keywords:
- ACPI_METHOD_SET_ARGUMENT_BUFFER マクロ ACPI デバイス
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c29600dc80179b5f8acd81536ff21457ea42103b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824062"
---
# <a name="acpi_method_set_argument_buffer-macro"></a>ACPI\_メソッド\_設定\_引数\_バッファーマクロ


ACPI\_メソッド\_設定\_引数\_BUFFER マクロは、データバッファーに指定されているカスタムデータに対して、 [**acpi\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)のメンバーを\_引数構造体に設定します。

<a name="syntax"></a>構文
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_BUFFER(
    Argument,
    BuffData,
    BuffLength
);
```

<a name="parameters"></a>パラメーター
----------

*引数*   
引数構造\_の ACPI\_メソッドへのポインター。

*BuffData*   
カスタムデータを格納するデータバッファーへのポインター。

*BuffLength*   
カスタムデータのサイズ (バイト単位)。

<a name="return-value"></a>戻り値
------------

このマクロは値を返しません。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して、カスタムデータを提供する引数の構造\_、ACPI\_メソッドのメンバーを設定できます。

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

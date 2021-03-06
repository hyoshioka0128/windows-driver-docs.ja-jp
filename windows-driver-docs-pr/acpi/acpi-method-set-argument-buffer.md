---
title: ACPI_METHOD_SET_ARGUMENT_BUFFER マクロ
description: ACPI_METHOD_SET_ARGUMENT_BUFFER マクロは、データ バッファーで指定されているカスタム データの ACPI_METHOD_ARGUMENT 構造体のメンバーを設定します。
ms.assetid: 1f335814-fa9f-45c6-b970-10884e971ec1
keywords:
- ACPI_METHOD_SET_ARGUMENT_BUFFER マクロ ACPI デバイス
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e7d3f5ca7ad3b58d471af4beb33cbf1eb33e6eb2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355877"
---
# <a name="acpimethodsetargumentbuffer-macro"></a>ACPI\_メソッド\_設定\_引数\_バッファー マクロ


ACPI\_メソッド\_設定\_引数\_バッファー マクロがのメンバーを設定、 [ **ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)データ バッファーで指定されているカスタム データの構造体。

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
ACPI へのポインター\_メソッド\_引数構造体。

*BuffData*   
カスタム データを格納するデータ バッファーへのポインター。

*BuffLength*   
カスタム データのバイト単位のサイズ。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>注釈
-------

ドライバーは、このマクロを使用して ACPI のメンバーを設定する\_メソッド\_カスタム データを提供する引数の構造体。

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


[**ACPI\_メソッド\_引数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 

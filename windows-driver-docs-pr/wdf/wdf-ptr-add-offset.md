---
title: WDF_PTR_ADD_OFFSET マクロ
description: WDF_PTR_ADD_OFFSET マクロは、アドレスにオフセット値を追加し、結果として得られるアドレスを返します。
ms.assetid: 21402be4-ef71-4828-b588-d178d66472e5
keywords:
- WDF_PTR_ADD_OFFSET マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d25e5af8889f724cfd0e345276a60869b980ef9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845414"
---
# <a name="wdf_ptr_add_offset-macro"></a>WDF_PTR_ADD_OFFSET マクロ


**WDF_PTR_ADD_OFFSET**マクロは、アドレスにオフセット値を追加し、結果として得られるアドレスを返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PVOID WDF_PTR_ADD_OFFSET(
    _ptr,
    _offset
);
```

<a name="parameters"></a>パラメーター
----------

*_ptr*   
アドレスを指定します。

*_offset*   
オフセット値をバイト単位で指定します。

<a name="return-value"></a>戻り値
------------

結果のアドレスへのポインターを返します。

<a name="remarks"></a>注釈
-------

このマクロは、 *_type*パラメーターを pvoid に設定して[**WDF_PTR_ADD_OFFSET_TYPE**](wdf-ptr-add-offset-type.md)を呼び出します。

マクロは次のように定義されます。

```ManagedCPlusPlus
#define WDF_PTR_ADD_OFFSET(_ptr, _offset) \
        WDF_PTR_ADD_OFFSET_TYPE(_ptr, _offset, PVOID)
```

次に示すのは、トースターサンプル (トースター\\func\\特集\\wmi) の例です。 この例では、ドライバーは**WDF_PTR_ADD_OFFSET**を呼び出して、 [**WDF_WMI_BUFFER_APPEND_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdf_wmi_buffer_append_string)関数に渡す宛先バッファーアドレスを決定するために、アドレスにオフセットを追加します。

```cpp
        //
        // Write the instance name
        //
        size -= wnodeSize;
        status = WDF_WMI_BUFFER_APPEND_STRING(
            WDF_PTR_ADD_OFFSET(wnode, wnode->OffsetInstanceName),
            size,
            &deviceName,
            &length
            );

        //
        // Size was precomputed, this should never fail
        //
        ASSERT(NT_SUCCESS(status));


        //
        // Write the data, which is the model name as a string
        //
        size -= wnodeInstanceNameSize;
        WDF_WMI_BUFFER_APPEND_STRING(
            WDF_PTR_ADD_OFFSET(wnode,  wnode->DataBlockOffset),
            size,
            &modelName,
            &length
            );
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td><p>最小 KMDF バージョン</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF バージョン</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfcore .h (Wdf を含む)</td>
</tr>
</tbody>
</table>











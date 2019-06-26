---
title: WDF_PTR_ADD_OFFSET macro
description: WDF_PTR_ADD_OFFSET マクロは、アドレスにオフセット値を追加し、結果として得られるアドレスを返します。
ms.assetid: 21402be4-ef71-4828-b588-d178d66472e5
keywords:
- WDF_PTR_ADD_OFFSET macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22116b3f13865a440689621f9c76353c43cae57b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372098"
---
# <a name="wdfptraddoffset-macro"></a>WDF_PTR_ADD_OFFSET macro


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
バイト オフセットの値を指定します。

<a name="return-value"></a>戻り値
------------

結果として得られるアドレスへのポインターを返します。

<a name="remarks"></a>注釈
-------

このマクロを呼び出す[ **WDF_PTR_ADD_OFFSET_TYPE** ](wdf-ptr-add-offset-type.md)で、*種類 (_t)* に PVOID パラメーターを設定します。

マクロの定義は次のとおりです。

```ManagedCPlusPlus
#define WDF_PTR_ADD_OFFSET(_ptr, _offset) \
        WDF_PTR_ADD_OFFSET_TYPE(_ptr, _offset, PVOID)
```

トースター サンプルから例を次に示します (トースター\\func\\機能を備えた\\wmi.c)。 例では、ドライバーが呼び出す**WDF_PTR_ADD_OFFSET**に渡す変換先バッファーのアドレスを決定するアドレスのオフセットを追加する、 [ **WDF_WMI_BUFFER_APPEND_STRING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/nf-wdfwmi-wdf_wmi_buffer_append_string)関数。

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

<a name="requirements"></a>必要条件
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
<td>Wdfcore.h (Wdf.h を含む)</td>
</tr>
</tbody>
</table>











---
title: WDF_PTR_ADD_OFFSET_TYPE macro
description: WDF_PTR_ADD_OFFSET_TYPE マクロは、アドレスにオフセット値を追加し、指定した型にキャストの結果として得られるアドレスを返します。
ms.assetid: b46d0bbe-8401-4c97-8327-fecd3af50eca
keywords:
- WDF_PTR_ADD_OFFSET_TYPE macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72632a005c9d2a2324d5c45977f6fef7a62f526c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366473"
---
# <a name="wdfptraddoffsettype-macro"></a>WDF_PTR_ADD_OFFSET_TYPE macro


**WDF_PTR_ADD_OFFSET_TYPE**マクロがアドレスにオフセット値を追加し、指定した型にキャストの結果として得られるアドレスを返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
_type WDF_PTR_ADD_OFFSET_TYPE(
    _ptr,
    _offset,
    _type
);
```

<a name="parameters"></a>パラメーター
----------

*_ptr*   
アドレスを指定します。

*_offset*   
バイト オフセットの値を指定します。

*_type*   
返されるデータ型を指定します。

<a name="return-value"></a>戻り値
------------

結果として得られるアドレスへのポインターを返します。 戻り値のデータ型を選択する、*種類 (_t)* マクロのパラメーター。

<a name="remarks"></a>注釈
-------

マクロの定義は次のとおりです。

```ManagedCPlusPlus
#define WDF_PTR_ADD_OFFSET_TYPE(_ptr, _offset, _type) \
    ((_type) (((PUCHAR) (_ptr)) + (_offset)))
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
<td>Wdfcore.h (Wdf.h を含む)</td>
</tr>
</tbody>
</table>

 

 







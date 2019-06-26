---
title: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE macro
description: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE マクロは、ドライバーの WDF_OBJECT_ATTRIBUTES 構造体を初期化し、構造にオブジェクトのドライバー定義のコンテキスト情報を挿入します。
ms.assetid: 83e397b1-e37d-451d-9007-3b34993187c3
keywords:
- WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c9df33b879048f74488cf33754471e49f5adb8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372114"
---
# <a name="wdfobjectattributesinitcontexttype-macro"></a>WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE macro


\[KMDF および UMDF に適用されます。\]

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**マクロ初期化ドライバーの[ **WDF_OBJECT_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体し、オブジェクトのドライバーが定義したコンテキストを挿入します。構造体に情報。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(
    _attributes,
    _contexttype
);
```

<a name="parameters"></a>パラメーター
----------

*方法を示します*   
ポインターを[ **WDF_OBJECT_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体。

*_contexttype*   
オブジェクトのコンテキストの領域の内容を記述したドライバー定義構造体の構造体の型名。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>注釈
-------

呼び出しの前に**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**、呼び出す必要があります[ **WDF_DECLARE_CONTEXT_TYPE** ](wdf-declare-context-type.md)または[ **WDF_DECLARE_CONTEXT_TYPE_WITH_NAME** ](wdf-declare-context-type-with-name.md)グローバルに (関数) 内ではありません。

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**マクロを組み合わせて、 [ **WDF_OBJECT_ATTRIBUTES_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdf_object_attributes_init)関数と[ **WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE** ](wdf-object-attributes-set-context-type.md)マクロ。

<a name="examples"></a>例
--------

次のコード例では、WDM_NDIS_REQUEST context 構造体を定義します。 例を起動し、 [ **WDF_DECLARE_CONTEXT_TYPE_WITH_NAME** ](wdf-declare-context-type-with-name.md)構造を登録し、コンテキストのアクセサー メソッドの名前を指定するマクロ**RequestGetMyContext**. 次に、関数の例では、割り当て、 [ **WDF_OBJECT_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造、および、初期化、 **WDF_OBJECT_ATTRIBUTES**構造体。

```cpp
typedef struct _WDM_NDIS_REQUEST
{
   PMP_ADAPTER  Adapter;
   NDIS_OID  Oid;
   NDIS_REQUEST_TYPE  RequestType;
   PVOID  InformationBuffer;
   ULONG  InformationBufferLength;
   PULONG  BytesReadOrWritten;
   PULONG  BytesNeeded;
} WDM_NDIS_REQUEST, *PWDM_NDIS_REQUEST;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(WDM_NDIS_REQUEST, RequestGetMyContext);

// above are in global space

...

WDF_OBJECT_ATTRIBUTES  attributes;

WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE( &attributes, WDM_NDIS_REQUEST );
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
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF バージョン</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject.h (Wdf.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)

[**WDF_OBJECT_ATTRIBUTES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdf_object_attributes_init)

[**WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE**](wdf-object-attributes-set-context-type.md)

 

 







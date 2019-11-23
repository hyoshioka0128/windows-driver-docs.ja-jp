---
title: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE マクロ
description: WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE マクロは、ドライバーの WDF_OBJECT_ATTRIBUTES 構造体を初期化し、オブジェクトのドライバー定義コンテキスト情報を構造体に挿入します。
ms.assetid: 83e397b1-e37d-451d-9007-3b34993187c3
keywords:
- WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6ac65c103f9e5fe49d365ae450b6627c94b2c56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845419"
---
# <a name="wdf_object_attributes_init_context_type-macro"></a>WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE マクロ


\[KMDF と UMDF\] に適用されます

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**マクロは、ドライバーの[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体を初期化し、オブジェクトのドライバー定義コンテキスト情報を構造体に挿入します。

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

*_attributes*   
[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体へのポインター。

*_contexttype*   
オブジェクトのコンテキスト空間の内容を記述するドライバー定義の構造体の構造体型の名前。

<a name="return-value"></a>戻り値
------------

このマクロは値を返しません。

<a name="remarks"></a>注釈
-------

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**を呼び出す前に、 [**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)または[**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)を (関数内ではなく) グローバルに呼び出す必要があります。

**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**マクロは、 [**WDF_OBJECT_ATTRIBUTES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)関数と[**WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE**](wdf-object-attributes-set-context-type.md)マクロを結合します。

<a name="examples"></a>例
--------

次のコード例では、WDM_NDIS_REQUEST コンテキスト構造を定義します。 次に、この例では、 [**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)マクロを呼び出して構造体を登録し、コンテキストアクセサーメソッドに**Requestgetmycontext**という名前を付けます。 次に、関数で、この例では[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体を割り当て、 **WDF_OBJECT_ATTRIBUTES**構造体を初期化します。

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
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF バージョン</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject .h (Wdf を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)

[**WDF_OBJECT_ATTRIBUTES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)

[**WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE**](wdf-object-attributes-set-context-type.md)

 

 







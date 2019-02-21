---
title: WdfObjectGetTypedContext マクロ
description: WdfObjectGetTypedContext マクロは、オブジェクトのコンテキストの領域へのポインターを返します。
ms.assetid: de0edae4-7c05-4419-972e-c106875dfff1
keywords:
- WdfObjectGetTypedContext マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64b9a86fff6d15e77189030c09a31ba47758aff8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548832"
---
# <a name="wdfobjectgettypedcontext-macro"></a>WdfObjectGetTypedContext マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectGetTypedContext**マクロが、オブジェクトのコンテキストの領域へのポインターを返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PVOID WdfObjectGetTypedContext(
    Handle,
    Type
);
```

<a name="parameters"></a>パラメーター
----------

*ハンドル*   
Framework のオブジェクトへのハンドル。

*型*   
オブジェクトのコンテキストの領域を記述するドライバー定義構造体のシンボル名。

<a name="return-value"></a>戻り値
------------

**WdfObjectGetTypedContext**指定されたオブジェクトのコンテキストの領域にポインターを返します。

<a name="remarks"></a>注釈
-------

使用することができます、 **WdfObjectGetTypedContext**マクロを任意のフレームワーク オブジェクト コンテキストの領域へのポインターを取得します。 このマクロを使用して、代わりに、オブジェクト固有のコンテキストのアクセサー メソッドを呼び出すことがによって作成された、 [ **WDF_DECLARE_CONTEXT_TYPE** ](wdf-declare-context-type.md)マクロまたは[ **WDF_DECLARE_CONTEXT_TYPE_WITH_NAME** ](wdf-declare-context-type-with-name.md)マクロ。 使用する場合**WdfObjectGetTypedContext**、使用することも必要があります WDF_DECLARE_CONTEXT_TYPE または WDF_DECLARE_CONTEXT_TYPE_WITH_NAME、オブジェクト コンテキストを宣言します。

これらのマクロの詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](https://msdn.microsoft.com/library/windows/hardware/ff542873)します。

<a name="examples"></a>例
--------

次のコード例では、要求オブジェクトのコンテキスト構造 (MY_REQUEST_CONTEXT) を定義し、構造体を登録します。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(MY_REQUEST_CONTEXT)
```

次のコード例では、要求オブジェクトを作成し、そのコンテキストの領域へのポインターを取得します。

```cpp
WDFREQUEST Request;
WDF_OBJECT_ATTRIBUTES MyRequestObjectAttributes;
PMY_REQUEST_CONTEXT pMyContext;

WDF_OBJECT_ATTRIBUTES_INIT(&amp;MyRequestObjectAttributes);
WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE(
                                       &amp;MyRequestObjectAttributes,
                                       MY_REQUEST_CONTEXT
                                       );
status = WdfRequestCreate(
                          &amp;MyRequestObjectAttributes,
                          NULL,
                          &amp;Request
                          );

if (!NT_SUCCESS(status)) {
    return status;
}
pMyContext = WdfObjectGetTypedContext(
                                      Request,
                                      MY_REQUEST_CONTEXT
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
<tr class="odd">
<td><p>Library</p></td>
<td>Wdf01000.sys (KMDF)。WUDFx02000.dll (UMDF)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>任意のレベル</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

[**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)

 

 







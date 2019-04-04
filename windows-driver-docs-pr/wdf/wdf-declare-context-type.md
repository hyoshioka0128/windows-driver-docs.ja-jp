---
title: WDF_DECLARE_CONTEXT_TYPE マクロ
description: WDF_DECLARE_CONTEXT_TYPE マクロは、名前とドライバーのオブジェクト固有のコンテキストの領域のアクセサー メソッドを作成します。
ms.assetid: 5fd9950e-943a-4340-b8f1-125343effdf7
keywords:
- WDF_DECLARE_CONTEXT_TYPE マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2193b23abfdd8a60a670fc14b627fbf1faf919
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570473"
---
# <a name="wdfdeclarecontexttype-macro"></a>WDF_DECLARE_CONTEXT_TYPE マクロ


\[KMDF および UMDF に適用されます。\]

WDF_DECLARE_CONTEXT_TYPE マクロは、名前とドライバーのオブジェクト固有のコンテキストの領域のアクセサー メソッドを作成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void WDF_DECLARE_CONTEXT_TYPE(
    _contexttype
);
```

<a name="parameters"></a>パラメーター
----------

*_contexttype*   
オブジェクトのコンテキストの領域の内容を記述したドライバー定義構造体の構造体の型名。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>コメント
-------

詳細については、このマクロを使用して、[フレームワーク オブジェクト コンテキストの空間](https://msdn.microsoft.com/library/windows/hardware/ff542873)を参照してください。

<a name="examples"></a>使用例
--------

次のコード例は、要求オブジェクトのコンテキスト構造 (MY_REQUEST_CONTEXT) を定義、構造体を登録し、WDF_DECLARE_CONTEXT_TYPE マクロを呼び出します。 マクロは、メソッドのコンテキストの構造と名前のアクセサー メソッドを作成します**WdfObjectGet_MY_REQUEST_CONTEXT**します。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(MY_REQUEST_CONTEXT)
```

次のコード例は、要求オブジェクトを作成し、次を使用して、 **WdfObjectGet_MY_REQUEST_CONTEXT**のアクセサー メソッドをオブジェクトのコンテキストの領域へのポインターを取得します。

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
                          &amp;MyRequestObjectAttributes
                          NULL,
                          &amp;Request
                          );
if (!NT_SUCCESS(status)) {
    return status;
}
pMyContext = WdfObjectGet_MY_REQUEST_CONTEXT(Request);
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


[**WdfObjectGetTypedContext**](wdfobjectgettypedcontext.md)

[**WDF_DECLARE_CONTEXT_TYPE_WITH_NAME**](wdf-declare-context-type-with-name.md)

 

 







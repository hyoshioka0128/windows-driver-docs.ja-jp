---
title: WDF_DECLARE_CONTEXT_TYPE_WITH_NAME マクロ
description: WDF_DECLARE_CONTEXT_TYPE_WITH_NAME マクロは、ドライバーのオブジェクト固有のコンテキストの領域の指定した名前のアクセサー メソッドを作成します。
ms.assetid: e5911bd2-6976-4a91-b9ba-befa7ec93103
keywords:
- WDF_DECLARE_CONTEXT_TYPE_WITH_NAME マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 266c7d6edd45efe2db07f665ebe7d237c32a7c8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372127"
---
# <a name="wdfdeclarecontexttypewithname-macro"></a>WDF_DECLARE_CONTEXT_TYPE_WITH_NAME マクロ


\[KMDF および UMDF に適用されます。\]

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME マクロは、ドライバーのオブジェクト固有のコンテキストの領域の指定した名前のアクセサー メソッドを作成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(
    _contexttype,
    _castingfunction
);
```

<a name="parameters"></a>パラメーター
----------

*_contexttype*   
オブジェクトのコンテキストの領域の内容を記述したドライバー定義構造体の構造体の型名。

*_castingfunction*   
C 言語ルーチンの名前。 マクロは、オブジェクトのコンテキストの領域を作成するアクセサー メソッドの名前として、この名前を使用します。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>コメント
-------

詳細については、このマクロを使用して、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-context-space)します。

<a name="examples"></a>使用例
--------

次のコード例では、要求オブジェクトの context 構造 (MY_REQUEST_CONTEXT) を定義します。 例が、構造体を登録し、コンテキストのアクセサー メソッドの名前を指定する WDF_DECLARE_CONTEXT_TYPE_WITH_NAME マクロを呼び出すし、 **RequestGetMyContext**します。

```cpp
typedef struct _MY_REQUEST_CONTEXT {
  LIST_ENTRY ListEntry;
  WDFMEMORY Memory;
} MY_REQUEST_CONTEXT, *PMY_REQUEST_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(MY_REQUEST_CONTEXT, RequestGetMyContext)
```

次のコード例は、要求オブジェクトを作成し、使用、 **RequestGetMyContext**のアクセサー メソッドをオブジェクトのコンテキストの領域へのポインターを取得します。

```cpp
WDFREQUEST Request;
WDF_OBJECT_ATTRIBUTES MyRequestObjectAttributes;
PMY_REQUEST_CONTEXT pMyContext;

WDF_OBJECT_ATTRIBUTES_INIT(&MyRequestObjectAttributes);
WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE(
                                       &MyRequestObjectAttributes,
                                       MY_REQUEST_CONTEXT
                                       );
status = WdfRequestCreate(
                          &MyRequestObjectAttributes
                          NULL,
                          &Request
                          );

if (!NT_SUCCESS(status)) {
    return status;
}

pMyContext = RequestGetMyContext(Request);
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

[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

 

 







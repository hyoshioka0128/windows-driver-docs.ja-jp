---
title: WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE macro
description: WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロは、オブジェクトの WDF_OBJECT_ATTRIBUTES 構造にオブジェクトのドライバー定義のコンテキスト情報を挿入します。
ms.assetid: cac8b8f4-cc6b-4e6c-ad0b-dee58e4673ff
keywords:
- WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6576bcf7e3c04dce211fdacc6cfc15b9c664ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390854"
---
# <a name="wdfobjectattributessetcontexttype-macro"></a>WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE macro


\[KMDF および UMDF に適用されます。\]

WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロは、オブジェクトのオブジェクトのドライバー定義のコンテキスト情報を挿入[ **WDF_OBJECT_ATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造体。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE(
    _attributes,
    _contexttype
);
```

<a name="parameters"></a>パラメーター
----------

*方法を示します*   
オブジェクトへのポインター [ **WDF_OBJECT_ATTRIBUTES** ](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造体。

*_contexttype*   
オブジェクトのコンテキストの領域の内容を記述したドライバー定義構造体の構造体の型名。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>コメント
-------

呼び出した後、WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロを使用する必要があります[ **WDF_OBJECT_ATTRIBUTES_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552402)します。

WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロの使用に関する詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](https://msdn.microsoft.com/library/windows/hardware/ff542873)します。

このマクロを使用するためのコード例を参照してください。 [ **WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)します。

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


[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

[**WDF_OBJECT_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff552400)

[**WDF_OBJECT_ATTRIBUTES_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552402)

[**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**](wdf-object-attributes-init-context-type.md)

 

 







---
title: WdfObjectAddCustomTypeWithData マクロ
description: WdfObjectAddCustomTypeWithData マクロとカスタムの型、framework のオブジェクトを関連付けるし、必要に応じてデータのバッファーとイベントのコールバック関数をこのペアを関連付けます。
ms.assetid: 237F9BAA-A2E2-4F20-B52E-8F093B326E45
keywords:
- WdfObjectAddCustomTypeWithData マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f81bf3e366d91547740e035434cac54a9699389b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390828"
---
# <a name="wdfobjectaddcustomtypewithdata-macro"></a>WdfObjectAddCustomTypeWithData マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectAddCustomTypeWithData**マクロとカスタムの型、framework のオブジェクトを関連付けるし、必要に応じてデータのバッファーとイベントのコールバック関数をこのペアを関連付けます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS WdfObjectAddCustomTypeWithData(
    _handle,
    _type,
    _data,
    _cleanup,
    _destroy
);
```

<a name="parameters"></a>パラメーター
----------

*_handle*   
Framework のオブジェクトへのハンドル。

*_type*   
カスタム型のドライバー定義の名前。

*_data*   
ドライバーが提供するデータ バッファーへのポインター。 このパラメーターは省略可能です。

*_cleanup*   
ドライバーへのポインター [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)コールバック関数、または NULL。 このパラメーターは省略可能です。

*_destroy*   
ドライバーへのポインター [ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)コールバック関数、または NULL。 このパラメーターは省略可能です。

<a name="return-value"></a>戻り値
------------

**WdfObjectAddCustomTypeWithData**操作が成功した場合に STATUS_SUCCESS を返します。 それ以外の場合、このメソッドでは、次の値のいずれかを返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>STATUS_OBJECT_PATH_INVALID</strong></td>
<td><p>指定したハンドルには、追加するカスタム型を含めることはできません。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td><p>カスタムの型を割り当てられませんでした。</p></td>
</tr>
<tr class="odd">
<td><strong>STATUS_OBJECT_NAME_EXISTS</strong></td>
<td><p>ドライバーでは、指定されたカスタム型は既に追加します。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_DELETE_PENDING</strong></td>
<td><p>Handle パラメーターを指定するオブジェクトを削除しています。 このような状況で、フレームワークは、カスタムの型を追加できません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ドライバーを呼び出す場合**WdfObjectAddCustomTypeWithData**データ バッファーへのポインター、ドライバーを提供できます、 [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)または[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)オブジェクトが削除されたときに、メモリ バッファーの割り当てを解除するコールバック関数。

オブジェクトのカスタム種類の詳細については、次を参照してください。 [Framework オブジェクトのカスタム型](https://msdn.microsoft.com/library/windows/hardware/hh406457)します。

コード例では、次を参照してください。 [ **WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)します。

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
<td><p>1.11</p></td>
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


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 







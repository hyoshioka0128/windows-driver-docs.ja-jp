---
title: WdfObjectAddCustomType マクロ
description: WdfObjectAddCustomType マクロは、カスタムの型を framework オブジェクトを関連付けます。
ms.assetid: 750CF669-A436-4571-B474-D5447E0AA64F
keywords:
- WdfObjectAddCustomType マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93403b63cc319393ba087b3af0c1d7be89fb3cb0
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161564"
---
# <a name="wdfobjectaddcustomtype-macro"></a>WdfObjectAddCustomType マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectAddCustomType**マクロは、カスタムの型と framework オブジェクトを関連付けます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS WdfObjectAddCustomType(
    _handle,
    _type
);
```

<a name="parameters"></a>パラメーター
----------

*_handle*   
Framework のオブジェクトへのハンドル。

*_type*   
カスタム型のドライバー定義の名前。

<a name="return-value"></a>戻り値
------------

**WdfObjectAddCustomType**操作が成功した場合に STATUS_SUCCESS を返します。 それ以外の場合、このメソッドでは、次の値のいずれかを返す可能性があります。

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

**WdfObjectAddCustomType**の簡易版です[ **WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)します。

オブジェクトのドライバーの種類の詳細については、次を参照してください。 [Framework オブジェクトのカスタム型](https://msdn.microsoft.com/library/windows/hardware/hh406457)します。

<a name="examples"></a>例
--------

このコード例では、カスタムの型をキューに追加する方法を示します。

```cpp
NTSTATUS                status;
WDF_IO_QUEUE_CONFIG     queueConfig;
WDFQUEUE                queue;  

WDF_IO_QUEUE_CONFIG_INIT(&queueConfig,   
                         WdfIoQueueDispatchParallel);  

status = WdfIoQueueCreate(device,  
                          &queueConfig,  
                          WDF_NO_OBJECT_ATTRIBUTES,  
                          &queue);  
 
if (!NT_SUCCESS(status)) {  
     TraceEvents(TRACE_LEVEL_ERROR, DBG_INFO,
                 "Failed to create queue, status=0x%x\n", status);
     goto Done;  
}  

status = WdfObjectAddCustomType(queue, TEST_TYPE1);  

if (!NT_SUCCESS(status)) {  
    TraceEvents(TRACE_LEVEL_ERROR, DBG_INFO,  
                "Failed to add TEST_TYPE1 to WDFOBJECT 0x%p, status=0x%x\n",   
    queue, status);  
    goto Done;  
}    

End:  
    return status;    
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

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 







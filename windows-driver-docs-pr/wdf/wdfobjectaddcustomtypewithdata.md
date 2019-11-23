---
title: WdfObjectAddCustomTypeWithData マクロ
description: WdfObjectAddCustomTypeWithData マクロは、フレームワークオブジェクトをカスタム型に関連付け、必要に応じて、このペアをデータバッファーとイベントコールバック関数に関連付けます。
ms.assetid: 237F9BAA-A2E2-4F20-B52E-8F093B326E45
keywords:
- WdfObjectAddCustomTypeWithData マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8180446bfe7a5bcf7a3cf20d6f27a4349adce9ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838773"
---
# <a name="wdfobjectaddcustomtypewithdata-macro"></a>WdfObjectAddCustomTypeWithData マクロ


\[KMDF と UMDF\] に適用されます

**WdfObjectAddCustomTypeWithData**マクロは、フレームワークオブジェクトをカスタム型に関連付け、必要に応じて、このペアをデータバッファーとイベントコールバック関数に関連付けます。

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
フレームワークオブジェクトへのハンドル。

*_type*   
カスタム型のドライバー定義名。

*_data*   
ドライバーによって提供されるデータバッファーへのポインター、または NULL。 このパラメーターはオプションです。

*_cleanup*   
ドライバーの[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)コールバック関数へのポインター、または NULL。 このパラメーターはオプションです。

*_destroy*   
ドライバーの[*Evtdestroycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)コールバック関数へのポインター、または NULL。 このパラメーターはオプションです。

<a name="return-value"></a>戻り値
------------

操作が成功した場合、 **WdfObjectAddCustomTypeWithData**は STATUS_SUCCESS を返します。 それ以外の場合、このメソッドは次のいずれかの値を返す可能性があります。

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
<td><p>指定されたハンドルにカスタム型を追加することはできません。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td><p>カスタム型を割り当てることができませんでした。</p></td>
</tr>
<tr class="odd">
<td><strong>STATUS_OBJECT_NAME_EXISTS</strong></td>
<td><p>ドライバーは、指定されたカスタム型を既に追加しています。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_DELETE_PENDING</strong></td>
<td><p>Handle パラメーターが指定するオブジェクトを削除しています。 この場合、フレームワークはカスタム型を追加しません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ドライバーがデータバッファーへのポインターを使用して**WdfObjectAddCustomTypeWithData**を呼び出す場合、ドライバーは、オブジェクトが削除されるときにメモリバッファーの割り当てを解除するための[*evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)または[*evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)コールバック関数を提供できます。

オブジェクトのカスタム型の詳細については、「[フレームワークオブジェクトのカスタム型](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-custom-types)」を参照してください。

コード例については、「 [**Wdfobjectaddcustomtype**](wdfobjectaddcustomtype.md)」を参照してください。

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
<td>Wdfobject .h (Wdf を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 







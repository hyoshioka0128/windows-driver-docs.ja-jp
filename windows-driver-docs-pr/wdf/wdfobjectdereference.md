---
title: WdfObjectDereference 参照マクロ
description: WdfObjectDereference 参照マクロは、指定されたフレームワークオブジェクトの参照カウントをデクリメントします。
ms.assetid: e945202c-7e6b-47b7-9216-d7a3a694489e
keywords:
- WdfObjectDereference 参照マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c0766856892b80bd9e870138792ed9f1f5d8414
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823926"
---
# <a name="wdfobjectdereference-macro"></a>WdfObjectDereference 参照マクロ


\[KMDF と UMDF\] に適用されます

**Wdfobjectdereference 参照**マクロは、指定されたフレームワークオブジェクトの参照カウントをデクリメントします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WdfObjectDereference(
  [in] WDFOBJECT Handle
);
```

<a name="parameters"></a>パラメーター
----------

\] での \[の*処理*  
フレームワークオブジェクトへのハンドル。

<a name="return-value"></a>戻り値
------------

なし。

バグチェックは、ドライバーが無効なオブジェクトハンドルを提供した場合に発生します。

<a name="remarks"></a>注釈
-------

オブジェクトの参照カウントが0になると、 **Wdfobjectdereference 参照**が返される前にオブジェクトが削除される可能性があります。

以前に[**Wdfobjectdereference**](wdfobjectreference.md)が呼び出されている場合にのみ、ドライバーは**Wdfobjectdereference**参照を呼び出すことができます。

[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)または[**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)を呼び出す代わりに、 **wdfobjectdereference 参照**を呼び出すことはできません。

オブジェクト参照カウントの詳細については、「[フレームワークオブジェクトのライフサイクル](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)」を参照してください。

<a name="examples"></a>例
--------

次のコード例では、オブジェクトの参照カウントをデクリメントします。

```cpp
WdfObjectDereference(Object); 
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
<tr class="odd">
<td><p>Library</p></td>
<td>Wdf01000 (KMDF);WUDFx02000 (UMDF)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI コンプライアンス規則</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate)"><strong>Drivercreate</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla)"><strong>MemAfterReqCompletedIoctlA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada)"><strong>MemAfterReqCompletedReadA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea)"><strong>MemAfterReqCompletedWriteA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueuefindrequestfailed" data-raw-source="[&lt;strong&gt;wdfioqueuefindrequestfailed&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueuefindrequestfailed)"><strong>wdfioqueuefindrequestfailed</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueueretrievefoundrequest" data-raw-source="[&lt;strong&gt;wdfioqueueretrievefoundrequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-wdfioqueueretrievefoundrequest)"><strong>wdfioqueueretrievefoundrequest</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)

[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)

[**WdfObjectReference**](wdfobjectreference.md)

 

 







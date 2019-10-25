---
title: WdfObjectReference マクロ
description: WdfObjectReference マクロは、指定されたフレームワークオブジェクトの参照カウントをインクリメントします。
ms.assetid: 8e024197-d366-4665-994b-4e03f559e017
keywords:
- WdfObjectReference マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58fbaf87d086c0df938421a1421715e136abf88c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845156"
---
# <a name="wdfobjectreference-macro"></a>WdfObjectReference マクロ


\[KMDF と UMDF\] に適用されます

**Wdfobjectreference**マクロは、指定されたフレームワークオブジェクトの参照カウントをインクリメントします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WdfObjectReference(
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

ドライバーが**Wdfobjectreference**を呼び出して参照カウントをインクリメントする場合、ドライバーは[**Wdfobjectreference**](wdfobjectdereference.md)参照を呼び出してカウントをデクリメントする必要があります。

**Wdfobjectreference**を呼び出す代わりに、ドライバーは[**Wdfobjectreferencewithtag**](wdfobjectreferencewithtag.md)または[**wdfobjectreferenceactual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual)を呼び出すことができます。

オブジェクト参照カウントの詳細については、「[フレームワークオブジェクトのライフサイクル](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)」を参照してください。

<a name="examples"></a>例
--------

次のコード例では、オブジェクトの参照カウントをインクリメントします。

```cpp
WdfObjectReference(Object); 
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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-drivercreate)"><strong>Drivercreate</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedintioctla)"><strong>MemAfterReqCompletedIntIoctlA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedioctla)"><strong>MemAfterReqCompletedIoctlA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedreada)"><strong>MemAfterReqCompletedReadA</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/kmdf-memafterreqcompletedwritea)"><strong>MemAfterReqCompletedWriteA</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WdfObjectReferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual)

[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)

 

 







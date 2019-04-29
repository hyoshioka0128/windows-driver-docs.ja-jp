---
title: WdfObjectDereference マクロ
description: 指定のフレームワーク オブジェクトの参照カウントを WdfObjectDereference マクロをデクリメントします。
ms.assetid: e945202c-7e6b-47b7-9216-d7a3a694489e
keywords:
- WdfObjectDereference マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef6c19f02441c777fa0f4c5c5cfa3116ce66bdcb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390821"
---
# <a name="wdfobjectdereference-macro"></a>WdfObjectDereference マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectDereference**マクロ フレームワークの指定したオブジェクトの参照カウントをデクリメントします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WdfObjectDereference(
  [in] WDFOBJECT Handle
);
```

<a name="parameters"></a>パラメーター
----------

*処理*\[で\]  
Framework のオブジェクトへのハンドル。

<a name="return-value"></a>戻り値
------------

なし。

バグ チェックでは、ドライバー、無効なオブジェクトのハンドルを提供する場合に発生します。

<a name="remarks"></a>コメント
-------

前に、オブジェクトが削除されるオブジェクトの参照カウントには、0 になると、 **WdfObjectDereference**を返します。

ドライバーが呼び出せる**WdfObjectDereference**が以前に呼び出された場合にのみ[ **WdfObjectReference**](wdfobjectreference.md)します。

呼び出す代わりに**WdfObjectDereference**、ドライバーが呼び出せる[ **WdfObjectDereferenceWithTag** ](wdfobjectdereferencewithtag.md)または[ **WdfObjectDereferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548743)します。

オブジェクトの参照カウントの詳細については、次を参照してください。 [Framework オブジェクトのライフ サイクル](https://msdn.microsoft.com/library/windows/hardware/ff542889)します。

<a name="examples"></a>使用例
--------

オブジェクトの参照カウントを次のコード例をデクリメントします。

```cpp
WdfObjectDereference(Object); 
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
<tr class="odd">
<td><p>Library</p></td>
<td>Wdf01000.sys (KMDF)。WUDFx02000.dll (UMDF)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 準拠の規則</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff544957" data-raw-source="[&lt;strong&gt;DriverCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544957)"><strong>DriverCreate</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549090" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIntIoctlA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549090)"> <strong>MemAfterReqCompletedIntIoctlA</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549106" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedIoctlA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549106)"> <strong>MemAfterReqCompletedIoctlA</strong></a>、<a href="https://msdn.microsoft.com/library/windows/hardware/ff549116" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedReadA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549116)"> <strong>MemAfterReqCompletedReadA</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549125" data-raw-source="[&lt;strong&gt;MemAfterReqCompletedWriteA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549125)"> <strong>MemAfterReqCompletedWriteA</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh975098" data-raw-source="[&lt;strong&gt;wdfioqueuefindrequestfailed&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh975098)"> <strong>wdfioqueuefindrequestfailed</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh975099" data-raw-source="[&lt;strong&gt;wdfioqueueretrievefoundrequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh975099)"> <strong>wdfioqueueretrievefoundrequest</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WdfObjectDereferenceActual**](https://msdn.microsoft.com/library/windows/hardware/ff548743)

[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)

[**WdfObjectReference**](wdfobjectreference.md)

 

 







---
title: WdfObjectReferenceWithTag マクロ
description: WdfObjectReferenceWithTag マクロは、指定されたフレームワークオブジェクトの参照カウントをインクリメントし、ドライバーの現在のファイル名と行番号を参照に割り当てます。 このマクロでは、参照にタグ値も割り当てられます。
ms.assetid: f0206238-c745-48b3-84d0-9f6d6ec9c2e0
keywords:
- WdfObjectReferenceWithTag マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85ac98cb6c57f9d448428b39626dd668fea1be63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843075"
---
# <a name="wdfobjectreferencewithtag-macro"></a>WdfObjectReferenceWithTag マクロ


\[KMDF と UMDF\] に適用されます

**Wdfobjectreferencewithtag**マクロは、指定されたフレームワークオブジェクトの参照カウントをインクリメントし、ドライバーの現在のファイル名と行番号を参照に割り当てます。 このマクロでは、参照にタグ値も割り当てられます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WdfObjectReferenceWithTag(
  [in] WDFOBJECT Handle,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>パラメーター
----------

\] での \[の*処理*  
フレームワークオブジェクトへのハンドル。

\] 内の*タグ*\[  
フレームワークがオブジェクト参照の識別タグとして格納するドライバー定義の値。

<a name="return-value"></a>戻り値
------------

なし。

バグチェックは、ドライバーが無効なオブジェクトハンドルを提供した場合に発生します。

<a name="remarks"></a>注釈
-------

ドライバーが**Wdfobjectreferencewithtag**を呼び出して参照カウントをインクリメントする場合、ドライバーは[**WdfObjectDereferenceWithTag**](wdfobjectdereferencewithtag.md)を呼び出してカウントをデクリメントする必要があります。

[**Wdfobjectreference**](wdfobjectreference.md)ではなく[**Wdfobjectreferenceactual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectreferenceactual)または**wdfobjectreferencewithtag**を呼び出すと、追加情報 (タグ値、行番号、ファイル名) が Microsoft デバッガーに提供されます。 **Wdfobjectreferenceactual**を使用すると、ドライバーは行番号とファイル名を指定でき、 **Wdfobjectreferencewithtag**はドライバーの現在の行番号とファイル名を使用します。

**! Wdftagtracker**デバッガー拡張機能を使用して、タグ、行番号、およびファイル名の値を表示できます。 デバッガー拡張機能は、ポインターと一連の文字の両方としてタグ値を表示します。 デバッガー拡張機能の詳細については、「 [KMDF ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)」を参照してください。

オブジェクト参照カウントの詳細については、「[フレームワークオブジェクトのライフサイクル](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)」を参照してください。

<a name="examples"></a>例
--------

次のコード例では、オブジェクトの参照カウントをインクリメントし、タグ値を参照に割り当てます。

```cpp
WdfObjectReferenceWithTag(
                          object,
                          pTag
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
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WdfObjectReference**](wdfobjectreference.md)

 

 







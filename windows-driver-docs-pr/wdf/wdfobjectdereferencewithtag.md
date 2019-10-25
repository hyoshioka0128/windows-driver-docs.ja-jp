---
title: WdfObjectDereferenceWithTag マクロ
description: WdfObjectDereferenceWithTag マクロは、指定されたフレームワークオブジェクトの参照カウントをデクリメントし、ドライバーの現在のファイル名と行番号を参照に割り当てます。 このマクロは、参照にタグ値も割り当てます。
ms.assetid: c5cfe516-ad62-4656-a033-d1800d9554a8
keywords:
- WdfObjectDereferenceWithTag マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e2af1195bf03fe3e875ff40b6a32c46b1efdf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842410"
---
# <a name="wdfobjectdereferencewithtag-macro"></a>WdfObjectDereferenceWithTag マクロ


\[KMDF と UMDF\] に適用されます

**WdfObjectDereferenceWithTag**マクロは、指定されたフレームワークオブジェクトの参照カウントをデクリメントし、ドライバーの現在のファイル名と行番号を参照に割り当てます。 このマクロは、参照にタグ値も割り当てます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WdfObjectDereferenceWithTag(
  [in] WDFOBJECT Handle,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>パラメーター
----------

\] での \[の*処理*  
フレームワークオブジェクトへのハンドル。

\] 内の*タグ*\[  
オブジェクト参照を識別するドライバー定義値。 タグ値は、ドライバーが以前に[**Wdfobjectreferencewithtag**](wdfobjectreferencewithtag.md)に指定したタグ値と一致している必要があります。

<a name="return-value"></a>戻り値
------------

なし。

バグチェックは、ドライバーが無効なオブジェクトハンドルを提供した場合に発生します。

<a name="remarks"></a>注釈
-------

オブジェクトの参照カウントが0になると、 **WdfObjectDereferenceWithTag**が返される前にオブジェクトが削除される可能性があります。

[**Wdfobjectdereference 参照**](wdfobjectdereference.md)の代わりに[**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)または**WdfObjectDereferenceWithTag**を呼び出すと、追加情報 (タグ文字列、行番号、およびファイル名) が Microsoft デバッガーに提供されます。 **WdfObjectDereferenceActual**では、ドライバーで行番号とファイル名を指定できます。 **WdfObjectDereferenceWithTag**では、ドライバーの現在の行番号とファイル名が使用されます。

**! Wdftagtracker**デバッガー拡張機能を使用して、タグ、行番号、およびファイル名の値を表示できます。 デバッガー拡張機能は、ポインターと一連の文字の両方としてタグ値を表示します。 デバッガー拡張機能の詳細については、「 [KMDF ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)」を参照してください。

オブジェクト参照カウントの詳細については、「[フレームワークオブジェクトのライフサイクル](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)」を参照してください。

<a name="examples"></a>例
--------

次のコード例では、オブジェクトの参照カウントをデクリメントし、タグ値を参照に割り当てます。

```cpp
WdfObjectDereferenceWithTag(
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


[**WdfObjectDereference 参照**](wdfobjectdereference.md)

[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)

 

 







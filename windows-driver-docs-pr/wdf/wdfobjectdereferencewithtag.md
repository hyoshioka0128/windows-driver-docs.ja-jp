---
title: WdfObjectDereferenceWithTag マクロ
description: オブジェクトを指定のフレームワークの参照カウント WdfObjectDereferenceWithTag マクロ デクリメントして、参照に、ドライバーの現在ファイル名と行番号を割り当てます。 このマクロは、参照にもタグ値を割り当てます。
ms.assetid: c5cfe516-ad62-4656-a033-d1800d9554a8
keywords:
- WdfObjectDereferenceWithTag マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d16fbc4afe3e1101881903c3a22d087192fef7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372090"
---
# <a name="wdfobjectdereferencewithtag-macro"></a>WdfObjectDereferenceWithTag マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectDereferenceWithTag**指定のフレームワークの参照カウントをデクリメントをマクロを選択し、オブジェクト参照に、ドライバーの現在ファイル名と行番号を割り当てます。 このマクロは、参照にもタグ値を割り当てます。

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

*処理*\[で\]  
Framework のオブジェクトへのハンドル。

*タグ*\[で\]  
オブジェクト参照を識別するドライバーの定義済みの値。 タグの値は、ドライバーは以前に指定されたタグの値と一致する必要があります[ **WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)します。

<a name="return-value"></a>戻り値
------------

なし。

バグ チェックでは、ドライバー、無効なオブジェクトのハンドルを提供する場合に発生します。

<a name="remarks"></a>注釈
-------

前に、オブジェクトが削除されるオブジェクトの参照カウントには、0 になると、 **WdfObjectDereferenceWithTag**を返します。

呼び出す[ **WdfObjectDereferenceActual** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)または**WdfObjectDereferenceWithTag**の代わりに[ **WdfObjectDereference** ](wdfobjectdereference.md) Microsoft デバッガーに追加の情報 (タグ文字列、行番号、およびファイル名) を提供します。 **WdfObjectDereferenceActual**中に、行番号とファイル名を指定するには、ドライバーは、 **WdfObjectDereferenceWithTag**ドライバーの現在の行番号とファイル名を使用します。

使用して、タグ、行番号、およびファイル名の値を表示することができます、 **! wdftagtracker**デバッガー拡張機能。 デバッガー拡張機能では、ポインターと、一連の文字の両方として、タグの値が表示されます。 詳細については、デバッガーの拡張機能は、次を参照してください。 [KMDF ドライバーをデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)します。

オブジェクトの参照カウントの詳細については、次を参照してください。 [Framework オブジェクトのライフ サイクル](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)します。

<a name="examples"></a>例
--------

次は、オブジェクトの参照カウントをデクリメントの例をコードし、タグ値を参照に代入します。

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
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WdfObjectDereference**](wdfobjectdereference.md)

[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)

 

 







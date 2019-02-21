---
title: WdfObjectReferenceWithTag マクロ
description: WdfObjectReferenceWithTag マクロは、指定のフレームワーク オブジェクトの参照カウントをインクリメントし、参照に、ドライバーの現在のファイル名と行番号を割り当てます。 マクロは、参照にもタグ値を割り当てます。
ms.assetid: f0206238-c745-48b3-84d0-9f6d6ec9c2e0
keywords:
- WdfObjectReferenceWithTag マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a4426aad88ad8466da6ce36a7bc84355db6af13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536900"
---
# <a name="wdfobjectreferencewithtag-macro"></a>WdfObjectReferenceWithTag マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectReferenceWithTag**マクロがフレームワークの指定したオブジェクトの参照カウントをインクリメントし、参照に、ドライバーの現在ファイル名と行番号を割り当てます。 マクロは、参照にもタグ値を割り当てます。

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

*処理*\[で\]  
Framework のオブジェクトへのハンドル。

*タグ*\[で\]  
フレームワークは、オブジェクト参照の識別タグとして格納するドライバーの定義済みの値。

<a name="return-value"></a>戻り値
------------

なし。

バグ チェックでは、ドライバー、無効なオブジェクトのハンドルを提供する場合に発生します。

<a name="remarks"></a>注釈
-------

ドライバーを呼び出す場合**WdfObjectReferenceWithTag**参照カウントをインクリメントするドライバーを呼び出す必要があります[ **WdfObjectDereferenceWithTag** ](wdfobjectdereferencewithtag.md)カウントをデクリメントします。

呼び出す[ **WdfObjectReferenceActual** ](https://msdn.microsoft.com/library/windows/hardware/ff548760)または**WdfObjectReferenceWithTag**の代わりに[ **WdfObjectReference**](wdfobjectreference.md) Microsoft デバッガーに追加の情報 (タグの値、行番号、およびファイル名) を提供します。 **WdfObjectReferenceActual**中に、行番号とファイル名を指定するには、ドライバーは、 **WdfObjectReferenceWithTag**ドライバーの現在の行番号とファイル名を使用します。

使用して、タグ、行番号、およびファイル名の値を表示することができます、 **! wdftagtracker**デバッガー拡張機能。 デバッガー拡張機能では、ポインターと、一連の文字の両方として、タグの値が表示されます。 詳細については、デバッガーの拡張機能は、次を参照してください。 [KMDF ドライバーをデバッグ](https://msdn.microsoft.com/library/windows/hardware/ff540790)します。

オブジェクトの参照カウントの詳細については、次を参照してください。 [Framework オブジェクトのライフ サイクル](https://msdn.microsoft.com/library/windows/hardware/ff542889)します。

<a name="examples"></a>例
--------

次のコード例では、オブジェクトの参照カウントをインクリメントし、参照にタグの値を割り当てます。

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


[**WdfObjectReference**](wdfobjectreference.md)

 

 







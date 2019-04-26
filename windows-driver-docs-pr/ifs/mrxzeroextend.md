---
title: MRxZeroExtend ルーチン
description: MRxZeroExtend ルーチンは、ネットワークのミニ リダイレクターがファイル システム オブジェクトの内容を切り捨てることを要求する RDBSS によって呼び出されます。
ms.assetid: d4a7c201-3c7d-40e9-a7da-17f40862c258
keywords:
- MRxZeroExtend ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxZeroExtend
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b13e646a2c9051ce9aeb320479779020143d3a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352946"
---
# <a name="mrxzeroextend-routine"></a>MRxZeroExtend ルーチン


*MRxZeroExtend*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクトの内容を切り捨てることを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxZeroExtend;

NTSTATUS MRxZeroExtend(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxZeroExtend*ステータスを返します\_次のよう、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンが実装されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*MRxZeroExtend*ファイル オブジェクトが削除のマークされていないと、ファイル オブジェクトは、ページング ファイルではない場合に、クリーンアップ操作の一部として呼び出されます。 *MRxZeroExtend*が呼び出され、有効なデータの長さとファイルのサイズの部分では、ゼロ拡張があることを確認します。 呼び出した後*MRxZeroExtend*、RDBSS セット、 **Header.ValidDataLength.QuadPart**等しく FCB 構造体の構造体のメンバー、 **Header.FileSize.QuadPart**FCB 構造体のメンバー。

呼び出し*MRxZeroExtend*への呼び出しに続いて[ **MRxCleanupFobx** ](https://msdn.microsoft.com/library/windows/hardware/ff549841)クリーンアップ操作の一部として。

戻り値を無視する RDBSS *MRxZeroExtend*します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxAreFilesAliased**](https://msdn.microsoft.com/library/windows/hardware/ff549838)

[**MRxCleanupFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549841)

[**MRxCloseSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff549845)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://msdn.microsoft.com/library/windows/hardware/ff549871)

[**MRxDeallocateForFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549872)

[**MRxExtendForCache**](https://msdn.microsoft.com/library/windows/hardware/ff549878)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

 

 







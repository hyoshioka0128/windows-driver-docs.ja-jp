---
title: MRxTruncate ルーチン
description: MRxTruncate ルーチンは、ネットワークのミニ リダイレクターがファイル システム オブジェクトの内容を切り捨てることを要求する RDBSS によって呼び出されます。
ms.assetid: d60ec8ef-2ccf-42ad-97d2-1aaf9d60acfb
keywords:
- MRxTruncate ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxTruncate
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 089a0f1759973a12500ec20eb787e9a776585727
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577896"
---
# <a name="mrxtruncate-routine"></a>MRxTruncate ルーチン


*MRxTruncate*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクトの内容を切り捨てることを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxTruncate;

NTSTATUS MRxTruncate(
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

*MRxTruncate*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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

 

<a name="remarks"></a>コメント
-------

*MRxTruncate*の両方の次の条件に該当する場合に、クリーンアップ操作の一部として呼び出されます。

-   ディスク ファイルまたはディレクトリに対応するファイル オブジェクト

-   これは、クリーンアップの最後の呼び出しと、切り捨てがマークされているファイル オブジェクト。

場合の切り捨て、ファイル オブジェクトがマークされている、 **fcbstate** FCB 構造体のメンバーが、FCB\_状態\_TRUNCATE\_ON\_閉じるビットが設定されます。 RDBSS は後でキャッシュのマップを初期化します。

呼び出し*MRxTruncate*への呼び出しに続いて[ **MRxCleanupFobx** ](https://msdn.microsoft.com/library/windows/hardware/ff549841)クリーンアップ操作の一部として。

戻り値を無視する RDBSS *MRxTruncate*します。

<a name="requirements"></a>必要条件
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

[**MRxZeroExtend**](mrxzeroextend.md)

 

 







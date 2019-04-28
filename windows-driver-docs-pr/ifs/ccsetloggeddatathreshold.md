---
title: CcSetLoggedDataThreshold ルーチン
description: CcSetLoggedDataThreshold ルーチンは、ダーティ ログ ページのスキャンは遅延書き込みを開始するときのしきい値を設定します。
ms.assetid: 067121C3-3BD6-48EA-BD8E-B28620F799E1
keywords:
- CcSetLoggedDataThreshold ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- CcSetLoggedDataThreshold
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4c2d13ee49f2ba986f1ed04ac3d05c5b4720425
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368583"
---
# <a name="ccsetloggeddatathreshold-routine"></a>CcSetLoggedDataThreshold ルーチン


[ **CcSetLoggedDataThreshold** ](ccistheredirtyloggedpages.md)ルーチンは、ログのダーティ ページのスキャンが遅延書き込みを開始する場合のしきい値を設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID CcSetLoggedDataThreshold(
  _In_ PVOID LogHandle,
  _In_ ULONG NumberOfPages
);
```

<a name="parameters"></a>パラメーター
----------

*LogHandle* \[in\]  
新しいしきい値のログのハンドル。

*NumberOfPages* \[で\]  
指定されたログのログのダーティ ページの数をしきい値*LogHandle*します。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

にしきい値*NumberOfPages*で値が返される場合にのみ使用されます、 *PercentageUsed*のパラメーター、 *QueryLogUsageRoutine*コールバック ルーチンは 0 です。 *QueryLogUsageRoutine*への呼び出しにコールバックが設定されて[ **CcSetLogHandleForFileEx**](ccsetloghandleforfileex.md)します。

[ **CcSetLoggedDataThreshold** ](ccistheredirtyloggedpages.md)ルーチンは、ログの完全な割合を使用しない場合、ログのダーティ ページの数の固定値を設定するために使用します。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または FltKernel.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CcSetLogHandleForFileEx**](ccsetloghandleforfileex.md)

 

 







---
title: CcSetLogHandleForFileEx ルーチン
description: CcSetLogHandleForFileEx ルーチンでは、関数は、ログ ファイルのファイルと追跡のコールバックをログ ハンドルを設定します。
ms.assetid: D56BEAC9-6AB8-44BA-ADFC-D2435A1458DB
keywords:
- CcSetLogHandleForFileEx ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- CcSetLogHandleForFileEx
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0709e0223fdf6ab65bcf094792ebeaf361666fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352198"
---
# <a name="ccsetloghandleforfileex-routine"></a>CcSetLogHandleForFileEx ルーチン


**CcSetLogHandleForFileEx**ルーチンは、ファイルと追跡のコールバックをログ ハンドル ファイル ログの機能を設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID CcSetLogHandleForFileEx(
  _In_ PFILE_OBJECT     FileObject,
  _In_ PVOID            LogHandle,
  _In_ PFLUSH_TO_LSN    FlushToLsnRoutine,
  _In_ PQUERY_LOG_USAGE QueryLogUsageRoutine
);
```

<a name="parameters"></a>パラメーター
----------

*FileObject* \[で\]ログ ハンドルを格納するファイルのファイル オブジェクトへのポインター。

*LogHandle* \[で\]が格納されるログのハンドルへのポインター。

*FlushToLsnRoutine* \[で\]ログ ファイルへのポインターがこのファイルのバッファーをフラッシュする前に呼び出すコールバック ルーチンをフラッシュします。 このルーチンが呼び出されてフラッシュされるすべてのバッファー制御ブロック (BCB) の最新の論理シーケンス番号 (LSN) をログ ファイルがフラッシュされるようにします。 このルーチンは、次のように宣言されます。

```cpp
typedef
VOID (*PFLUSH_TO_LSN) (
            IN PVOID LogHandle,
            IN LARGE_INTEGER Lsn
            );
```

<a href="" id="loghandle"></a>
***LogHandle***

このクライアントを識別するために使用される非透過構造へのポインター。

<a href="" id="lsn"></a>
***Lsn***

このコールバック ルーチンからの戻り値ではディスクにする必要がある LSN です。

*QueryLogUsageRoutine* \[で\]このファイルのログの使用率を取得するために呼び出すクライアント コールバック ルーチンへのポインター。 このルーチンは、確認のダーティ ページの書き込みを開始するしきい値が満たされたかどうかに呼び出されます。 このルーチンは、次のように宣言されます。

```cpp
typedef  
VOID (*PQUERY_LOG_USAGE) (  
            IN PVOID LogHandle,  
            OUT PUSHORT PercentageFull  
            );  
```

<a href="" id="loghandle"></a>
***LogHandle***

このクライアントを識別するために使用される非透過構造へのポインター。

<a href="" id="percentagefull"></a>
***PercentageFull***

ログの使用量の割合を示す 0 から 100 までの値。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**CcSetLogHandleForFileEx**後続の呼び出しで使用するためのファイルのログ ハンドルを設定します[ **CcGetDirtyPages**](https://msdn.microsoft.com/library/windows/hardware/ff539088)します。

コールバックを*FlushToLsnRoutine*と*QueryLogUsageRoutine*が必要です。 これらの値では、NULL は指定できません。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8 以降で利用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
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
<td align="left"><p>任意のレベル</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CcGetDirtyPages**](https://msdn.microsoft.com/library/windows/hardware/ff539088)

[**CcSetDirtyPinnedData**](https://msdn.microsoft.com/library/windows/hardware/ff539211)

 

 







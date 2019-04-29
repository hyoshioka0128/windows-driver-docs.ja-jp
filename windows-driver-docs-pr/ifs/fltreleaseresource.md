---
title: FltReleaseResource ルーチン
description: FltReleaseResource ルーチンでは、現在のスレッドによって所有されている、指定したリソースを解放します。
ms.assetid: 2884c596-77ec-4cba-b6cb-000d96cc6342
keywords:
- FltReleaseResource ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FltReleaseResource
api_location:
- fltmgr.sys
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 003edbcd3b87b06cffecaaa566befc096e2878b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393021"
---
# <a name="fltreleaseresource-routine"></a>FltReleaseResource ルーチン


**FltReleaseResource**ルーチンは、現在のスレッドによって所有されている、指定したリソースを解放します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID FltReleaseResource(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>パラメーター
----------

*リソース*\[入力、出力\]  
リソースが解放される非透過のスケジュール作成構造体へのポインター。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**FltReleaseResource**が前に呼び出すことによって取得したリソースが解放[ **FltAcquireResourceExclusive** ](fltacquireresourceexclusive.md)または[ **FltAcquireResourceShared**](fltacquireresourceshared.md)します。

**FltReleaseResource**用のラッパーです[ **ExReleaseResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545597)通常カーネル APC 配信を再び有効にします。

**FltReleaseResource**通常カーネル APC の配信を再有効化を呼び出す必要はありません[ **KeLeaveCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552964)または[ **FsRtlExitFileSystem** ](fsrtlexitfilesystem.md)呼び出した後**FltReleaseResource**します。

リソースへの排他アクセスを取得するために呼び出す[ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)します。

共有アクセス用のリソースを取得するために呼び出す[ **FltAcquireResourceShared**](fltacquireresourceshared.md)します。

システムのリソースの一覧からリソースを削除する[ **ExDeleteResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff544578)します。

再利用するためのリソースを初期化するために呼び出す[ **ExReinitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545542)します。

次の構造体の詳細については、次を参照してください。 [÷ リソース ルーチンの概要](https://msdn.microsoft.com/library/windows/hardware/ff548046)でカーネルのアーキテクチャの設計ガイド。

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
<td align="left"><p>このルーチンは Microsoft Windows XP SP2、Microsoft Windows Server 2003 SP1 で使用できる以降。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">FltMgr.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Fltmgr.sys</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ExDeleteResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff544578)

[**ExInitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545317)

[**ExReinitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545542)

[**ExReleaseResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545597)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)

 

 







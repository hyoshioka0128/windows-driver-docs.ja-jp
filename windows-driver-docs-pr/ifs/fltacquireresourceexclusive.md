---
title: FltAcquireResourceExclusive ルーチン
description: FltAcquireResourceExclusive ルーチンでは、呼び出し元のスレッドによって、指定されたリソースへの排他アクセスを取得します。
ms.assetid: 3736582e-33eb-4967-acfa-4b9d2b8cd87f
keywords:
- FltAcquireResourceExclusive ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FltAcquireResourceExclusive
api_location:
- fltMgr.lib
- fltMgr.dll
api_type:
- LibDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca534dd7983147fe3ea971d3bf86bc5a8eee7815
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532215"
---
# <a name="fltacquireresourceexclusive-routine"></a>FltAcquireResourceExclusive ルーチン


**FltAcquireResourceExclusive**ルーチンは、呼び出し元のスレッドによって、指定されたリソースへの排他アクセスを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID FltAcquireResourceExclusive(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>パラメーター
----------

*リソース*\[入力、出力\]  
非透過のスケジュール作成構造体へのポインター。 この構造体の非ページ プールから呼び出し元が割り当てたを呼び出すことによって初期化する必要があります[ **ExInitializeResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545317)または[ **ExReinitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545542).

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

このルーチンは、Windows XP Service Pack 2 (SP2)、Windows Server 2003 Service Pack 1 (SP1)、および以降のバージョンの Windows で使用できます。

**FltAcquireResourceExclusive**呼び出し元のスレッドによって、指定されたリソースへの排他アクセスを取得します。

次の状況は、呼び出し元には、指定されたリソースに排他アクセスが与えられるかを決定します。

-   リソースが現在所有されていない場合、現在のスレッドに排他アクセスがすぐに付与します。

-   呼び出し元がリソースを取得して排他アクセスのため、同じ種類のアクセスを再帰的に、現在のスレッドが許可されます。

-   共有リソースにアクセスしている呼び出し元は、ロックを解除し、しのみ再取得する必要があります。

-   別のスレッドによって、排他として、リソースが現在所有している場合、または呼び出し元のみが共有されている場合、リソースへのアクセスは、リソースを取得するまでに、現在のスレッドが待機状態に配置されます。

&gt; \[!注\] &gt; 2 つのスレッドが同じリソースに対して共有ロックを保持し、その共有ロックを解放しないまま排他的ロックを取得しようと両方、デッドロックが発生します。 つまり、共有ロックを保持する他の各スレッドが待機および、までは、その他の共有保持は解放もします。

 

**FltAcquireResourceExclusive**用のラッパーです[ **ExAcquireResourceExclusiveLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544351)通常カーネル APC 配信を無効にします。

**FltAcquireResourceExclusive**通常カーネル APC の配信を無効にしますを呼び出す必要はありません[ **KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)または[ 。**FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)呼び出す前に**FltAcquireResourceExclusive**します。

呼び出すには、取得した後は、リソースを解放、 [ **FltReleaseResource**](fltreleaseresource.md)します。 すべての成功した呼び出し**FltAcquireResourceExclusive**後続の呼び出しによって照合される必要があります**FltReleaseResource**します。

共有アクセス用のリソースを取得するために呼び出す[ **FltAcquireResourceShared**](fltacquireresourceshared.md)します。

システムのリソースの一覧からリソースを削除する[ **ExDeleteResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff544578)します。

再利用するためのリソースを初期化するために呼び出す[ **ExReinitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545542)します。

次の構造体の詳細については、次を参照してください。 [÷ リソース ルーチンの概要](https://msdn.microsoft.com/library/windows/hardware/ff548046)でカーネルのアーキテクチャの設計ガイド。

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
<td align="left"><p>Windows XP SP2、Windows Server 2003 SP1、および以降のバージョンのすべての Windows オペレーティング システムで使用できます。</p></td>
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
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExDeleteResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff544578)

[**ExInitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545317)

[**ExReinitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545542)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552021)

 

 







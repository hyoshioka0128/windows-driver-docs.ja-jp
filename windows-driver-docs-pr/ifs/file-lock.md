---
title: FILE_LOCK 構造体
description: オペレーティング システムは不透明なファイルを使用して\_ファイルのロックをサポートする構造体をロックします。
ms.assetid: 89df2075-c542-4105-847f-9bc7ae4dab50
keywords:
- FILE_LOCK 構造インストール可能なファイル システム ドライバー
- PFILE_LOCK 構造体ポインター インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FILE_LOCK
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e36561ba15d2881dc145be7df0dd6cc3b9e395fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386079"
---
# <a name="filelock-structure"></a>ファイル\_ロック構造体


オペレーティング システムは不透明なファイルを使用して\_ファイルのロックをサポートする構造体をロックします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _FILE_LOCK {
  PCOMPLETE_LOCK_IRP_ROUTINE CompleteLockIrpRoutine;
  PUNLOCK_ROUTINE            UnlockRoutine;
  BOOLEAN                    FastIoIsQuestionable;
  BOOLEAN                    SpareC[3];
  PVOID                      LockInformation;
  FILE_LOCK_INFO             LastReturnedLockInfo;
  PVOID                      LastReturnedLock;
  volatile LONG              LockRequestsInProgress;
} FILE_LOCK, *PFILE_LOCK;
```

<a name="members"></a>Members
-------

**CompleteLockIrpRoutine**  
システムの使用に予約されています。

**UnlockRoutine**  
システムの使用に予約されています。

**FastIoIsQuestionable**  
システムの使用に予約されています。

**SpareC**  
システムの使用に予約されています。

**LockInformation**  
システムの使用に予約されています。

**LastReturnedLockInfo**  
システムの使用に予約されています。

**LastReturnedLock**  
システムの使用に予約されています。

**LockRequestsInProgress**  
システムの使用に予約されています。

<a name="remarks"></a>注釈
-------

ファイル システム ドライバー、従来のファイル システム フィルター ドライバーおよびミニフィルターに対して、作成してファイルを使用するさまざまなルーチンを使用できます\_ロック オブジェクトでもファイルへの読み取り/書き込みアクセスをテストします。

-   ファイルを割り当てる\_ロック オブジェクト、呼び出し[ **FsRtlAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[ **FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)します。

-   初期化されていない、ファイルを初期化するために\_ロック オブジェクト、呼び出し[ **FsRtlInitializeFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)または[ **FltInitializeFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializefilelock). 注意をファイル\_から返されるロック[ **FsRtlAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[ **FltAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)は既に初期化されます。

-   ファイルの初期化解除に\_ロック オブジェクト、呼び出し[ **FsRtlUninitializeFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)または[ **FltUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuninitializefilelock)します。

-   ファイルを解放する\_ロック オブジェクトによって割り当てられる、 [ **FsRtlAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock) 、ルーチンの呼び出し[ **FsRtlFreeFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock). ファイルを解放する\_ロック オブジェクトによって割り当てられる、 [ **FltAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock) 、ルーチンの呼び出し[ **FltFreeFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreefilelock).

ファイルの後に\_ロックがれました初期化、ルーチンなど[ **FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)、 [ **FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)、および[ **FsRtlFastCheckLockForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforread)ファイルを他のスレッドによってアクセスできるかどうかを判断するために使用できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Microsoft Windows 2000、および以降のバージョンの Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (FltKernel.h または Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializefilelock)

**FltInitializeFileLock**
[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFastCheckLockForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforread)

[**FsRtlFastCheckLockForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforwrite)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

 

 







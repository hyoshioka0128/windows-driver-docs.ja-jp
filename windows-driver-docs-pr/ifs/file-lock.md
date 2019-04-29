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
ms.openlocfilehash: a744b35346b16758aecb7754b375c4c2caa880f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383837"
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

<a name="members"></a>メンバー
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

-   ファイルを割り当てる\_ロック オブジェクト、呼び出し[ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)または[ **FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)します。

-   初期化されていない、ファイルを初期化するために\_ロック オブジェクト、呼び出し[ **FsRtlInitializeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff546122)または[ **FltInitializeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff543273). 注意をファイル\_から返されるロック[ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)または[ **FltAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff541743)は既に初期化されます。

-   ファイルの初期化解除に\_ロック オブジェクト、呼び出し[ **FsRtlUninitializeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547313)または[ **FltUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff544595)します。

-   ファイルを解放する\_ロック オブジェクトによって割り当てられる、 [ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640) 、ルーチンの呼び出し[ **FsRtlFreeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff546011). ファイルを解放する\_ロック オブジェクトによって割り当てられる、 [ **FltAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff541743) 、ルーチンの呼び出し[ **FltFreeFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff542969).

ファイルの後に\_ロックがれました初期化、ルーチンなど[ **FsRtlCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545758)、 [ **FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)、および[ **FsRtlFastCheckLockForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff545918)ファイルを他のスレッドによってアクセスできるかどうかを判断するために使用できます。

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


[**FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)

[**FltCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541834)

[**FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)

[**FltInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543273)

**FltInitializeFileLock**
[**FsRtlAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff545640)

[**FsRtlCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545758)

[**FsRtlCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545760)

[**FsRtlFastCheckLockForRead**](https://msdn.microsoft.com/library/windows/hardware/ff545918)

[**FsRtlFastCheckLockForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff545928)

[**FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)

[**FsRtlUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547313)

 

 







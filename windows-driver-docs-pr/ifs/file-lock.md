---
title: FILE_LOCK 構造体
description: オペレーティングシステムは、ファイルのロックをサポートするために、不透明なファイル\_ロック構造を使用します。
ms.assetid: 89df2075-c542-4105-847f-9bc7ae4dab50
keywords:
- FILE_LOCK 構造のインストール可能なファイルシステムドライバー
- PFILE_LOCK 構造体ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 83107e9bbcda813da1c5777456635778c5599601
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841415"
---
# <a name="file_lock-structure"></a>ファイル\_ロック構造


オペレーティングシステムは、ファイルのロックをサポートするために、不透明なファイル\_ロック構造を使用します。

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
システム用に予約されています。

**UnlockRoutine**  
システム用に予約されています。

**問題あり**  
システム用に予約されています。

**SpareC**  
システム用に予約されています。

**LockInformation**  
システム用に予約されています。

**LastReturnedLockInfo**  
システム用に予約されています。

**LastReturnedLock**  
システム用に予約されています。

**LockRequestsInProgress**  
システム用に予約されています。

<a name="remarks"></a>注釈
-------

ファイルシステムドライバー、レガシファイルシステムフィルタードライバーおよびミニフィルターでは、さまざまなルーチンを使用して、ファイル\_ロックオブジェクトを作成および使用したり、ファイルへの読み取り/書き込みアクセスをテストしたりすることができます。

-   ファイル\_ロックオブジェクトに割り当てるには、 [**Fsrtlallocatefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)を呼び出します。

-   初期化されていないファイル\_ロックオブジェクトを初期化するには、 [**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)または[**Fltinitializefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)を呼び出します。 [**Fsrtlallocatefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)から返されたファイル\_ロックは既に初期化されていることに注意してください。

-   オブジェクト\_ロックを解除するには、 [**Fsrtluninitializefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)または[**fltuninitializefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializefilelock)を呼び出します。

-   [**Fsrtlallocatefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)ルーチンによって割り当てられるファイル\_ロックオブジェクトを解放するには、 [**Fsrtlfreefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)を呼び出します。 [**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)ルーチンによって割り当てられるファイル\_ロックオブジェクトを解放するには、 [**Fltfreefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreefilelock)を呼び出します。

ファイル\_ロックが初期化された後、 [**Fsrtlchecklockforreadaccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)、 [**fltchecklockforwriteaccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)、 [**Fsrtlchecklockforreadaccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforread)などのルーチンを使用して、他のスレッドがファイルにアクセスできるかどうかを判断できます。

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
<td align="left"><p>Microsoft Windows 2000、およびそれ以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (FltKernel .h または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)

**Fltinitializefilelock**
[ **Fsrtlallocatefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFastCheckLockForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforread)

[**FsRtlFastCheckLockForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfastchecklockforwrite)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

 

 







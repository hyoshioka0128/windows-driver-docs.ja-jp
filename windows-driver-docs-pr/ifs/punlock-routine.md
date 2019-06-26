---
title: PUNLOCK\_ルーチンの関数ポインター
description: フィルター (レガシ フィルターまたはミニフィルター) は、PUNLOCK を登録できます\_ファイルのフィルターの UnlockRoutine コールバック ルーチンとしてルーチンに型指定されたルーチン\_ロック構造体。
ms.assetid: e188bc88-e3dd-49d3-9c79-8eb408cd0338
keywords:
- PUNLOCK_ROUTINE 関数ポインター インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- UnlockRoutine
api_location:
- ntifs.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b2a17e00b62e20983b31336667888de6bd25cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385145"
---
# <a name="punlockroutine-function-pointer"></a>PUNLOCK\_ルーチンの関数ポインター


フィルター (レガシ フィルターまたはミニフィルター) は、PUNLOCK を登録できます\_として、フィルターのルーチンに型指定されたルーチン*UnlockRoutine*ファイル コールバック ルーチン\_ロック構造体。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef VOID ( *UnlockRoutine)(
  _In_ PVOID           Context,
  _In_ PFILE_LOCK_INFO FileLockInfo
);
```

<a name="parameters"></a>パラメーター
----------

*コンテキスト*\[で\]  
渡されたコンテキスト ポインター [ **FltProcessFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltprocessfilelock)または[ **FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)します。

*FileLockInfo* \[in\]  
ファイルへのポインターを非透過\_ロック\_バイト範囲ロックの情報の構造体。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

(レガシ フィルターまたはミニフィルター) フィルターを指定できます、PUNLOCK\_として、フィルターのルーチンに型指定されたルーチン*UnlockRoutine*ファイルのバイト範囲ロックのコールバック。

フィルターが指定されている場合、 *UnlockRoutine*ファイルの日常的な\_ロック構造では、ファイルにロックされているバイトの範囲から、ロックが削除されたときにこのルーチンは呼び出されます。

ミニフィルターとしてルーチンへのポインターを渡すことによってこのルーチンを指定します、 *UnlockRoutine*パラメーター [ **FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)します。

レガシ フィルターとしてルーチンへのポインターを渡すことによってこのルーチンを指定します、 *UnlockRoutine*パラメーター [ **FsRtlAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[ **FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)します。

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
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreefilelock)

[**FltInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializefilelock)

[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FltUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuninitializefilelock)

[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PCOMPLETE\_ロック\_IRP\_ルーチン**](pcomplete-lock-irp-routine.md)

[**PFLT\_完了\_ロック\_コールバック\_データ\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_complete_lock_callback_data_routine)

 

 







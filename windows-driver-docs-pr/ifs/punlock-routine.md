---
title: PUNLOCK\_ルーチン関数ポインター
description: フィルター (レガシフィルターまたはミニフィルター) では、PUNLOCK\_ルーチンで型指定されたルーチンを、ファイル\_ロック構造のフィルターの UnlockRoutine コールバックルーチンとして登録できます。
ms.assetid: e188bc88-e3dd-49d3-9c79-8eb408cd0338
keywords:
- PUNLOCK_ROUTINE 関数ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 609b70a5dbd8bc35b0cccd721ea0ba0a19272e65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841016"
---
# <a name="punlock_routine-function-pointer"></a>PUNLOCK\_ルーチン関数ポインター


フィルター (レガシフィルターまたはミニフィルター) では、PUNLOCK\_ルーチンで型指定されたルーチンを、ファイル\_ロック構造のフィルターの*UnlockRoutine*コールバックルーチンとして登録できます。

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

\] の*コンテキスト*\[  
[**Fltprocessfilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock)または[**fsrtlprocessfilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)に渡されたコンテキストポインター。

\] の*Filelockinfo* \[  
バイト範囲ロックのロック\_情報構造体を\_ファイルへの非透過的ポインター。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

フィルター (レガシフィルターまたはミニフィルター) では、必要に応じて PUNLOCK\_ルーチン型のルーチンを、バイト範囲のファイルロックのフィルターの*UnlockRoutine*コールバックとして指定できます。

ファイル\_ロック構造の*UnlockRoutine*ルーチンをフィルターが指定した場合、このルーチンは、ロックがファイル内のロックされたバイト範囲から削除されるときに呼び出されます。

ミニパスでは、 [**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)の*UnlockRoutine*パラメーターとしてルーチンへのポインターを渡すことによって、このルーチンを指定します。

レガシフィルターでは、 [**Fsrtlallocatefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)の*UnlockRoutine*パラメーターとしてルーチンへのポインターを渡すことによって、このルーチンを指定します。

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
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreefilelock)

[**FltInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltinitializefilelock)

[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FltUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuninitializefilelock)

[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PCOMPLETE\_ロック\_IRP\_ルーチン**](pcomplete-lock-irp-routine.md)

[**PFLT\_\_ロック\_コールバック\_データ\_ルーチンの完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_complete_lock_callback_data_routine)

 

 







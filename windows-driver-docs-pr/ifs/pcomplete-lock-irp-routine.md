---
title: PCOMPLETE\_ロック\_IRP\_ルーチンルーチン
description: ファイルシステムフィルタードライバー (レガシフィルター) は、フィルターの CompleteLockIrpRoutine コールバックとして、IRP\_ルーチン型のルーチン\_、PCOMPLETE\_ロックを登録できます。
ms.assetid: 400ff351-5906-4e6e-a708-e71441afe3b8
keywords:
- CompleteLockIrpRoutine のインストール可能なファイルシステムドライバー
- PCOMPLETE_LOCK_IRP_ROUTINE
topic_type:
- apiref
api_name:
- CompleteLockIrpRoutine
api_location:
- ntifs.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dfa49f57d705f42176307686debca2939c61daf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841040"
---
# <a name="pcomplete_lock_irp_routine-routine"></a>PCOMPLETE\_ロック\_IRP\_ルーチンルーチン


ファイルシステムフィルタードライバー (レガシフィルター) は、フィルターの*Completelockirproutine*コールバックとして、IRP\_ルーチン型のルーチン\_、pcomplete\_ロックを登録できます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PCOMPLETE_LOCK_IRP_ROUTINE CompleteLockIrpRoutine;

NTSTATUS CompleteLockIrpRoutine(
  _In_ PVOID Context,
  _In_ PIRP  Irp
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

\] の*コンテキスト*\[  
[**Fsrtlprocessfilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)に渡されたコンテキストポインター。

\] の*Irp* \[  
ファイルロックの irp [ **\_MJ\_ロック\_制御**](irp-mj-lock-control.md)要求を完了しています。 ロック要求の種類は、次のいずれかになります。

IRP\_\_ロック

IRP\_\_ロック解除\_すべて

IRP\_、\_キーによってすべての\_\_ロック解除\_

IRP\_\_のロック解除\_SINGLE

<a name="return-value"></a>戻り値
------------

このルーチンは、STATUS\_SUCCESS または適切な NTSTATUS 値を返します。 成功コードではない NTSTATUS 値が返された場合、ファイルのロックがファイルから削除されます。

<a name="remarks"></a>注釈
-------

ファイルシステムフィルタードライバー (レガシフィルター) では、必要に応じて、PCOMPLETE\_ロック\_IRP\_ルーチン型のルーチンを、バイト範囲のファイルロックのための従来のフィルターの*Completelockirproutine*ルーチンとして指定できます。

このルーチンを指定するために、レガシフィルターは[**Fsrtlallocatefilelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)の*Completelockirproutine*パラメーターとしてルーチンへのポインターを渡します。

レガシフィルターでファイルロックに対して*Completelockirprine*ルーチンが指定されている場合、 [**IRP\_MJ\_ロック\_制御**](irp-mj-lock-control.md)操作がファイルロックに対して実行されると、システムはこのルーチンを呼び出します。

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
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PUNLOCK\_ルーチン**](punlock-routine.md)

 

 







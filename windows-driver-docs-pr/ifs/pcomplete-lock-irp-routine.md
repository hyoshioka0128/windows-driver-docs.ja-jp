---
title: PCOMPLETE\_ロック\_IRP\_ルーチン ルーチン
description: ファイル システム フィルター ドライバー (レガシ フィルター)、PCOMPLETE を登録できます\_ロック\_IRP\_として、フィルターの CompleteLockIrpRoutine コールバック ルーチンに型指定されたルーチン。
ms.assetid: 400ff351-5906-4e6e-a708-e71441afe3b8
keywords:
- CompleteLockIrpRoutine ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: bfcbe5acc8aa646816652cd9e5c2ec153eeaecd0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386063"
---
# <a name="pcompletelockirproutine-routine"></a>PCOMPLETE\_ロック\_IRP\_ルーチン ルーチン


ファイル システム フィルター ドライバー (レガシ フィルター)、PCOMPLETE を登録できます\_ロック\_IRP\_として、フィルターのルーチンに型指定されたルーチン*CompleteLockIrpRoutine*コールバック。

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

*コンテキスト*\[で\]  
渡されたコンテキスト ポインター [ **FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)します。

*Irp* \[で\]  
ファイル ロックの IRP [ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)遂行される要求。 ロック要求の種類は、次のいずれかになります。

IRP\_MN\_LOCK

IRP\_MN\_UNLOCK\_ALL

IRP\_MN\_UNLOCK\_すべて\_BY\_キー

IRP\_MN\_UNLOCK\_単一

<a name="return-value"></a>戻り値
------------

このルーチンは、ステータスを返します\_成功または適切な NTSTATUS 値。 成功コードではない NTSTATUS 値が返された場合、ファイルのロックは、ファイルから削除されます。

<a name="remarks"></a>注釈
-------

ファイル システム フィルター ドライバー (レガシ フィルター) を指定できます、PCOMPLETE\_ロック\_IRP\_のレガシ フィルターとしてルーチンに型指定されたルーチン*CompleteLockIrpRoutine*の日常的なバイト範囲のファイルのロック。

このルーチンを指定するには、レガシ フィルターでは、としてルーチンにポインターを渡します、 *CompleteLockIrpRoutine*パラメーター [ **FsRtlAllocateFileLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)または[ **FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)します。

レガシ フィルターを指定する場合、 *CompleteLockIrpRoutine*ファイル ロックを日常的なシステム ルーチンを呼び出すこの完了したときに、 [ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)ファイル ロックを操作します。

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
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FsRtlAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlallocatefilelock)

[**FsRtlCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforreadaccess)

[**FsRtlCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlchecklockforwriteaccess)

[**FsRtlFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlfreefilelock)

[**FsRtlInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlinitializefilelock)

[**FsRtlProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprocessfilelock)

[**FsRtlUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtluninitializefilelock)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PUNLOCK\_ルーチン**](punlock-routine.md)

 

 







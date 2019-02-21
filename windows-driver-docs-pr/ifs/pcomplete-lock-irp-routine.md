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
ms.openlocfilehash: e8a40500a0655403aa3746edb4f3692e690c63cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538022"
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
渡されたコンテキスト ポインター [ **FsRtlProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547166)します。

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

このルーチンを指定するには、レガシ フィルターでは、としてルーチンにポインターを渡します、 *CompleteLockIrpRoutine*パラメーター [ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)または[ **FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)します。

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


[**FsRtlAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff545640)

[**FsRtlCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545758)

[**FsRtlCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545760)

[**FsRtlFreeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546011)

[**FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)

[**FsRtlProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547166)

[**FsRtlUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547313)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PUNLOCK\_ルーチン**](punlock-routine.md)

 

 







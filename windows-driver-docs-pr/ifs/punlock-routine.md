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
ms.openlocfilehash: ed4463eae98b835194329754512cab784cb81601
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573257"
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
渡されたコンテキスト ポインター [ **FltProcessFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff543427)または[ **FsRtlProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547166)します。

*FileLockInfo* \[in\]  
ファイルへのポインターを非透過\_ロック\_バイト範囲ロックの情報の構造体。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>コメント
-------

(レガシ フィルターまたはミニフィルター) フィルターを指定できます、PUNLOCK\_として、フィルターのルーチンに型指定されたルーチン*UnlockRoutine*ファイルのバイト範囲ロックのコールバック。

フィルターが指定されている場合、 *UnlockRoutine*ファイルの日常的な\_ロック構造では、ファイルにロックされているバイトの範囲から、ロックが削除されたときにこのルーチンは呼び出されます。

ミニフィルターとしてルーチンへのポインターを渡すことによってこのルーチンを指定します、 *UnlockRoutine*パラメーター [ **FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)します。

レガシ フィルターとしてルーチンへのポインターを渡すことによってこのルーチンを指定します、 *UnlockRoutine*パラメーター [ **FsRtlAllocateFileLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545640)または[ **FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)します。

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


[**FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)

[**FltCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541834)

[**FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)

[**FltFreeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff542969)

[**FltInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543273)

[**FltProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543427)

[**FltUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff544595)

[**FsRtlAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff545640)

[**FsRtlCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545758)

[**FsRtlCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff545760)

[**FsRtlFreeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546011)

[**FsRtlInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff546122)

[**FsRtlProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547166)

[**FsRtlUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547313)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PCOMPLETE\_ロック\_IRP\_ルーチン**](pcomplete-lock-irp-routine.md)

[**PFLT\_完了\_ロック\_コールバック\_データ\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551073)

 

 







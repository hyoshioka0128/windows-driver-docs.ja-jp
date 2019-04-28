---
title: FLT_PARAMETERS IRP_MJ_LOCK_CONTROL 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_ロック\_コントロール。
ms.assetid: 4dbdb4c8-5908-40e5-b600-225b47118c6d
keywords:
- FLT_PARAMETERS IRP_MJ_LOCK_CONTROL 共用体インストール可能なファイル システム ドライバー
- FLT_PARAMETERS union インストール可能なファイル システム ドライバー
- PFLT_PARAMETERS 共用体ポインター インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a84304a4abd2e921a06c0e78d7886651d1a45b1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364986"
---
# <a name="fltparameters-for-irpmjlockcontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_ロック\_コントロール共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作は構造体[ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PLARGE_INTEGER          Length;
    ULONG POINTER_ALIGNMENT Key;
    LARGE_INTEGER           ByteOffset;
    PEPROCESS               ProcessId;
    BOOLEAN                 FailImmediately;
    BOOLEAN                 ExclusiveLock;
  } LockControl;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**LockControl**  
次のメンバーを含む構造体。

**長さ**  
ロックする範囲のバイト単位の長さを指定する変数へのポインター。

**[キー]**  
バイト範囲ロックに割り当てられるキーの値。

**ByteOffset**  
ロックする範囲のファイル内のバイト オフセットを開始しています。

**プロセス Id**  
バイト範囲ロックが要求されたプロセスのプロセス ID を非透過のポインター。

**FailImmediately**  
すぐに、ロックを許可できない場合、ロック要求を失敗させるかどうかを示すブール値。 このメンバーに設定されている**FALSE**要求スレッドは、要求が許可されるまで待機状態に配置できる場合または**TRUE**できない場合。

**ExclusiveLock**  
排他ロックが要求されたかどうかを示すブール値。 このメンバーに設定されている**TRUE**排他ロックが要求された場合または**FALSE**共有ロックが要求された場合。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)用の構造、 [ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)構造体。

IRP\_MJ\_ロック\_IRP ベースの I/O 操作または I/O 操作が高速コントロールであることができます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**アクセス\_マスク**](https://msdn.microsoft.com/library/windows/hardware/ff540466)

[**アクセス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff538840)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltAllocateFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff541743)

[**FltCheckLockForReadAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541834)

[**FltCheckLockForWriteAccess**](https://msdn.microsoft.com/library/windows/hardware/ff541837)

[**FltFreeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff542969)

[**FltInitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543273)

[**FltProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543427)

[**FltUninitializeFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff544595)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PFLT\_完了\_ロック\_コールバック\_データ\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551073)

[**PUNLOCK\_ルーチン**](punlock-routine.md)

 

 







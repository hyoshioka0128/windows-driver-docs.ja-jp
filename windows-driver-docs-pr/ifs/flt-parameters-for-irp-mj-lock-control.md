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
ms.openlocfilehash: e7c2f7741283770aa656a4fbe36ba4a89842dec4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380344"
---
# <a name="fltparameters-for-irpmjlockcontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_ロック\_コントロール共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作は構造体[ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)します。

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

<a name="members"></a>Members
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

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)用の構造、 [ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)コールバック データによって表される操作 ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体。

IRP\_MJ\_ロック\_IRP ベースの I/O 操作または I/O 操作が高速コントロールであることができます。

<a name="requirements"></a>必要条件
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


[**アクセス\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**アクセス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltAllocateFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatefilelock)

[**FltCheckLockForReadAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforreadaccess)

[**FltCheckLockForWriteAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltchecklockforwriteaccess)

[**FltFreeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreefilelock)

[**FltInitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltinitializefilelock)

[**FltProcessFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltprocessfilelock)

[**FltUninitializeFileLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuninitializefilelock)

[**IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md)

[**PFLT\_完了\_ロック\_コールバック\_データ\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_complete_lock_callback_data_routine)

[**PUNLOCK\_ルーチン**](punlock-routine.md)

 

 







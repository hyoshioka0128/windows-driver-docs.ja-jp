---
title: FLT_PARAMETERS IRP_MJ_SYSTEM_CONTROL 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_システム\_コントロール。
ms.assetid: 6f1c34b2-1c79-4372-8b94-afe4b50294d5
keywords:
- FLT_PARAMETERS IRP_MJ_SYSTEM_CONTROL 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 4753ecccdad52d6f03845e3c85f791f79896725b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380484"
---
# <a name="fltparameters-for-irpmjsystemcontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_システム\_コントロール共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が IRP\_MJ\_システム\_コントロール。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG_PTR ProviderId;
    PVOID     DataPath;
    ULONG     BufferSize;
    PVOID     Buffer;
  } WMI;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**WMI**  
次のメンバーを含む構造体。

**ProviderId**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

**データパス**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

**BufferSize**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

**Buffer**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (詳しくは、次の「解説」を参照してください)。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP の構造\_MJ\_システム\_管理操作には、システム コントロールの操作のパラメーターが含まれています。コールバック データによって表される ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP の意味\_MJ\_システム\_制御パラメーターは、マイナー関数コードによって異なります。 (を参照してください、 **MinorFunction**のメンバー、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造です)。詳細については、次の小さな関数のコードに対して参照エントリを参照してください。

[**IRP\_MN\_変更\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)

[**IRP\_MN\_変更\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)

[**IRP\_MN\_DISABLE\_COLLECTION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)

[**IRP\_MN\_を無効にする\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)

[**IRP\_MN\_ENABLE\_COLLECTION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)

[**IRP\_MN\_を有効にする\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)

[**IRP\_MN\_EXECUTE\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)

[**IRP\_MN\_クエリ\_すべて\_データ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)

[**IRP\_MN\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)

[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)

[**IRP\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)

IRP\_MJ\_システム\_コントロールが IRP ベースの操作。

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


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MN\_変更\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)

[**IRP\_MN\_変更\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)

[**IRP\_MN\_DISABLE\_COLLECTION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)

[**IRP\_MN\_を無効にする\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)

[**IRP\_MN\_ENABLE\_COLLECTION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)

[**IRP\_MN\_を有効にする\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)

[**IRP\_MN\_EXECUTE\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)

[**IRP\_MN\_クエリ\_すべて\_データ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)

[**IRP\_MN\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)

[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)

[**IRP\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)

 

 







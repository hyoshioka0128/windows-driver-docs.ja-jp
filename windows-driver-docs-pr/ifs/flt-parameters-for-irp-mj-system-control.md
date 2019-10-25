---
title: IRP_MJ_SYSTEM_CONTROL 共用体の FLT_PARAMETERS
description: 操作の FLT\_IO\_パラメーター\_ブロック構造の MajorFunction フィールドが IRP\_MJ\_システム\_コントロールである場合に使用される共用体コンポーネント。
ms.assetid: 6f1c34b2-1c79-4372-8b94-afe4b50294d5
keywords:
- IRP_MJ_SYSTEM_CONTROL union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
- FLT_PARAMETERS union にインストール可能なファイルシステムドライバー
- PFLT_PARAMETERS union ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 33ffaaa9582216a58117b1f909e8147736113782
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841338"
---
# <a name="flt_parameters-for-irp_mj_system_control-union"></a>IRP\_MJ\_システム\_コントロール共用体の FLT\_パラメーター


操作の[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MAJORFUNCTION**フィールドが IRP\_MJ\_システム\_コントロールである場合に使用される共用体コンポーネント。

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
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (次の「解説」を参照してください)。

**データパス**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (次の「解説」を参照してください)。

**BufferSize**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (次の「解説」を参照してください)。

**格納**  
このパラメーターの意味は、操作のマイナー関数コードによって異なります。 (次の「解説」を参照してください)。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_システム\_制御操作の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) によって表されるシステム制御操作のためのパラメーターが含まれています。データ. これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_システム\_制御パラメーターの意味は、マイナー関数のコードによって異なります。 ( [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**minorfunction**メンバーを参照してください)。詳細については、次のマイナー関数コードの参照エントリを参照してください。

[**IRP\_\_1 つの\_インスタンス\_変更**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)

[**IRP\_\_1 つの\_項目\_変更**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)

[**IRP\_\_\_コレクションを無効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)

[**IRP\_\_\_イベントを無効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)

[**IRP\_\_\_コレクションを有効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)

[**IRP\_\_\_イベントを有効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)

[**IRP\_\_メソッドを実行\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)

[**IRP\_\_クエリ\_すべての\_データ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)

[**IRP\_\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)

[**IRP\_\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)

[**IRP\_\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)

IRP\_MJ\_システム\_制御は、IRP ベースの操作です。

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
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_\_1 つの\_インスタンス\_変更**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)

[**IRP\_\_1 つの\_項目\_変更**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)

[**IRP\_\_\_コレクションを無効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)

[**IRP\_\_\_イベントを無効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)

[**IRP\_\_\_コレクションを有効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)

[**IRP\_\_\_イベントを有効にする**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)

[**IRP\_\_メソッドを実行\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)

[**IRP\_\_クエリ\_すべての\_データ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)

[**IRP\_\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)

[**IRP\_\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)

[**IRP\_\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)

 

 







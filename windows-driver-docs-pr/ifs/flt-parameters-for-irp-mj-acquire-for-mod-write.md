---
title: IRP_MJ_ACQUIRE_FOR_MOD_WRITE 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_ACQUIRE_FOR_MOD_WRITE の場合、次の共用体コンポーネントが使用されます。
ms.assetid: f950f8df-fcaa-4af7-9227-eb069f289176
keywords:
- IRP_MJ_ACQUIRE_FOR_MOD_WRITE union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: d858766c0077e99e988dd3296d8b81c05176d597
ms.sourcegitcommit: b9a65cb309bea3d35048968bdc708e0067276e68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68313213"
---
# <a name="fltparameters-for-irpmjacquireformodwrite-union"></a>IRP_MJ_ACQUIRE_FOR_MOD_WRITE 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MAJORFUNCTION**フィールドが IRP_MJ_ACQUIRE_FOR_MOD_WRITE の場合、次の共用体コンポーネントが使用されます。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PLARGE_INTEGER EndingOffset;
    PERESOURCE     *ResourceToRelease;
  } AcquireForModifiedPageWriter;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>Members

```AcquireForModifiedPageWriter```

次のメンバーを含む構造体。

```EndingOffset```

書き込まれた最後のバイトのオフセットに1を加えた値を格納する変数へのポインター。

```ResourceToRelease```

取得する[リソース (リソース](https://docs.microsoft.com/windows-hardware/drivers/kernel/eresource-structures)) へのポインターへのポインター。

## <a name="remarks"></a>コメント

IRP_MJ_ACQUIRE_FOR_MOD_WRITE 操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) structure には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される**AcquireForModifiedPageWriter**操作のパラメーターが含まれています。 [**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

IRP_MJ_ACQUIRE_FOR_MOD_WRITE は、ファイルシステム (FSFilter) コールバック操作です。 この操作では、 *ResourceToRelease*は取得 (操作前) または取得された (操作後の) リソースへのポインターへのポインターです。 リソースは IRP_MJ_RELEASE_FOR_MOD_WRITE コールバック操作で解放されます。

FSFilter のコールバック操作の詳細については、 [**Fsrtlregisterfilesystemfiltercallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)のリファレンスエントリを参照してください。

## <a name="requirements"></a>必要条件

|   |   |
| - | - |
| Header | *Fltkernel .h* ( *fltkernel. h を*含む) |

## <a name="see-also"></a>関連項目

[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)

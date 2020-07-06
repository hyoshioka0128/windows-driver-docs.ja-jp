---
title: IRP_MJ_ACQUIRE_FOR_MOD_WRITE 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_ACQUIRE_FOR_MOD_WRITE 場合は、次の共用体コンポーネントが使用されます。
ms.assetid: f950f8df-fcaa-4af7-9227-eb069f289176
keywords:
- IRP_MJ_ACQUIRE_FOR_MOD_WRITE ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- PFLT_PARAMETERS 共用体ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 6aba803d9023e95a2b74fcd55909c94f1da83ca6
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968351"
---
# <a name="flt_parameters-for-irp_mj_acquire_for_mod_write-union"></a>IRP_MJ_ACQUIRE_FOR_MOD_WRITE 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが IRP_MJ_ACQUIRE_FOR_MOD_WRITE 場合は、次の共用体コンポーネントが使用されます。

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

## <a name="members"></a>メンバー

```AcquireForModifiedPageWriter```

次のメンバーを含む構造体。

```EndingOffset```

書き込まれた最後のバイトのオフセットに1を加えた値を格納する変数へのポインター。

```ResourceToRelease```

取得する[リソース (リソース](https://docs.microsoft.com/windows-hardware/drivers/kernel/eresource-structures)) へのポインターへのポインター。

## <a name="remarks"></a>注釈

IRP_MJ_ACQUIRE_FOR_MOD_WRITE 操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される**AcquireForModifiedPageWriter**操作のパラメーターが含まれています。 これは[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

IRP_MJ_ACQUIRE_FOR_MOD_WRITE は、ファイルシステム (FSFilter) コールバック操作です。 この操作では、 *ResourceToRelease*は取得 (操作前) または取得された (操作後の) リソースへのポインターへのポインターです。 リソースは IRP_MJ_RELEASE_FOR_MOD_WRITE コールバック操作で解放されます。

FSFilter のコールバック操作の詳細については、 [**Fsrtlregisterfilesystemfiltercallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)のリファレンスエントリを参照してください。

## <a name="requirements"></a>要件

**ヘッダー**: *fltkernel .H* ( *fltkernel .h を*含む)


## <a name="see-also"></a>関連項目

[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)

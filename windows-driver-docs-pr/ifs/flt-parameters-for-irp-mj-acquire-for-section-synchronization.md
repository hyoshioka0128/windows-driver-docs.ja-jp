---
title: IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 場合は、次の共用体コンポーネントが使用されます。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: a203d01aec8f6f30bf6d260259392b5b77852fd4
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968353"
---
# <a name="flt_parameters-for-irp_mj_acquire_for_section_synchronization-union"></a>IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 場合は、次の共用体コンポーネントが使用されます。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    FS_FILTER_SECTION_SYNC_TYPE SyncType;
    ULONG POINTER_ALIGNMENT     PageProtection;
    PFS_FILTER_SECTION_SYNC_OUTPUT OutputInformation;
  } AcquireForSectionSynchronization;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>メンバー

### <a name="synctype"></a>SyncType  

セクションに要求された同期の種類。 セクションが作成されている場合、このパラメーターは**SyncTypeCreateSection**に設定されます。それ以外の場合は、 **Synctypeother**に設定されます。

### <a name="pageprotection"></a>PageProtection

セクションに要求されたページ保護の種類。 **Synctype**が SyncTypeOther の場合、は0である必要があります。 それ以外の場合、このパラメーターは、定義されている[メモリ保護定数値](https://docs.microsoft.com/windows/win32/memory/memory-protection-constants)のいずれかである必要があります。

### <a name="outputinformation"></a>OutputInformation

作成されるセクションの属性を記述する情報を指定する[**FS_FILTER_SECTION_SYNC_OUTPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fs_filter_section_sync_output)構造体。

## <a name="remarks"></a>注釈

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される**AcquireForSectionSynchronization**操作のパラメーターが含まれています。 これは FLT_IO_PARAMETER_BLOCK 構造体に含まれています。

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION は、ファイルシステム (FSFilter) コールバック操作です。

**Synctype**メンバーの列挙値が**synctypeother**に設定されている場合、ファイルシステムミニフィルタードライバーまたはレガシフィルタードライバーがこの操作を失敗させることはできません。 **Synctype**が**SyncTypeCreateSection**に設定されている場合は、セクションを作成するのに十分なメモリがない場合、ファイルシステムミニフィルターまたはレガシフィルタードライバーが失敗し、STATUS_INSUFFICIENT_RESOURCES エラーが発生します。

FSFilter のコールバック操作の詳細については、 [**Fsrtlregisterfilesystemfiltercallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)のリファレンスエントリを参照してください。

## <a name="requirements"></a>要件

**バージョン**: windows XP 以降のバージョンの windows オペレーティングシステムで使用できます。

**ヘッダー**: fltkernel .H (fltkernel .h を含む)


## <a name="see-also"></a>関連項目

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)

---
title: IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION の場合、次の共用体コンポーネントが使用されます。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 7a379a78263a001816c4e4ad28815685faec231e
ms.sourcegitcommit: b9a65cb309bea3d35048968bdc708e0067276e68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68313214"
---
# <a name="fltparameters-for-irpmjacquireforsectionsynchronization-union"></a>IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MAJORFUNCTION**フィールドが IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION の場合、次の共用体コンポーネントが使用されます。

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

## <a name="members"></a>Members

### <a name="synctype"></a>SyncType  

セクションに要求された同期の種類。 セクションが作成されている場合、このパラメーターは**SyncTypeCreateSection**に設定されます。それ以外の場合は、 **Synctypeother**に設定されます。

### <a name="pageprotection"></a>PageProtection

セクションに要求されたページ保護の種類。 **Synctype**が SyncTypeOther の場合、は0である必要があります。 それ以外の場合、このパラメーターは、定義されている[メモリ保護定数値](https://docs.microsoft.com/windows/win32/memory/memory-protection-constants)のいずれかである必要があります。

### <a name="outputinformation"></a>OutputInformation

作成されるセクションの属性を記述する情報を指定する[**FS_FILTER_SECTION_SYNC_OUTPUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fs_filter_section_sync_output)構造体。

## <a name="remarks"></a>コメント

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) structure には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) によって表される**AcquireForSectionSynchronization**操作のパラメーターが含まれています。データ. FLT_IO_PARAMETER_BLOCK 構造体に含まれています。

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION は、ファイルシステム (FSFilter) コールバック操作です。

**Synctype**メンバーの列挙値が**synctypeother**に設定されている場合、ファイルシステムミニフィルタードライバーまたはレガシフィルタードライバーがこの操作を失敗させることはできません。 **Synctype**が**SyncTypeCreateSection**に設定されている場合、セクションを作成するのに十分なメモリがない場合、ファイルシステムミニフィルターまたはレガシフィルタードライバーは STATUS_INSUFFICIENT_RESOURCES エラーで失敗することがあります。

FSFilter のコールバック操作の詳細については、 [**Fsrtlregisterfilesystemfiltercallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)のリファレンスエントリを参照してください。

## <a name="requirements"></a>必要条件

| | |
| ------- | ------- |
| バージョン | Windows XP 以降のバージョンの Windows オペレーティングシステムで使用できます。 |
| Header    | Fltkernel .h (Fltkernel. h を含む) |

## <a name="see-also"></a>関連項目

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)

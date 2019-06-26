---
title: FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体
description: 次の共用体のコンポーネントは、操作の FLT_IO_PARAMETER_BLOCK 構造の MajorFunction フィールドは IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION ときに使用されます。
ms.assetid: ea3ae072-4a98-48df-871a-cc7d882b96b8
keywords:
- FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体インストール可能なファイル システム ドライバー
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
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: d5cd06b99e01e03e897aac2982e01418cb9eb251
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386075"
---
# <a name="fltparameters-for-irpmjacquireforsectionsynchronization-union"></a>FLT_PARAMETERS IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 共用体

次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT_IO_PARAMETER_BLOCK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block) IRP_MJ_ACQUIRE_FOR_SECTION_ の操作には構造体同期します。

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

セクションの必要な同期の種類。 このパラメーターに設定されている**SyncTypeCreateSection**セクションが作成されている場合、それ以外の場合に設定されて**SyncTypeOther**します。

### <a name="pageprotection"></a>PageProtection

セクションの要求されたページ保護の種類。 場合は 0 にする必要があります**SyncType** SyncTypeOther です。 それ以外の場合、このパラメーターは、おそらく PAGE_NOCACHE と組み合わせて、次のフラグのいずれかに指定できます。

| Value | 説明 |
| ----- | ------- |
| PAGE_READONLY | アクセスを読み取り専用または書き込み時コピーします。 |
| PAGE_READWRITE | 書き込み時コピー、または読み取り/書き込みのアクセス、読み取り専用です。 |
| PAGE_WRITECOPY | アクセスを読み取り専用または書き込み時コピーします。 PAGE_READONLY と等価です。 |
| PAGE_EXECUTE | アクセスを実行します。 |

### <a name="outputinformation"></a>OutputInformation

A [ **FS_FILTER_SECTION_SYNC_OUTPUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fs_filter_section_sync_output)構造が作成されているセクションの属性を説明する情報を指定します。

## <a name="remarks"></a>注釈

[ **FLT_PARAMETERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION 操作のための構造体のパラメーターを格納する、 **AcquireForSectionSynchronization**コールバック データによって表される操作 ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT_IO_PARAMETER_BLOCK 構造体が含まれています。

IRP_MJ_ACQUIRE_FOR_SECTION_SYNCHRONIZATION は、ファイル システム (FSFilter) コールバック操作です。

場合の列挙値、 **SyncType**に設定されているメンバー **SyncTypeOther**、ファイル システム ミニフィルターまたはレガシ フィルター ドライバーをこの操作に失敗することはできません。 場合**SyncType**に設定されている**SyncTypeCreateSection**、作成するための十分なメモリがない場合は、STATUS_INSUFFICIENT_RESOURCES エラーで失敗するファイル システム ミニフィルターまたはレガシ フィルター ドライバーが許可されている、セクション。

FSFilter コールバック操作の詳細については、参照のエントリを参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)します。

## <a name="requirements"></a>必要条件

| | |
| ------- | ------- |
| バージョン | Windows XP および Windows オペレーティング システムの以降のバージョンで使用できます。 |
| Header    | Fltkernel.h (Fltkernel.h を含む) |

## <a name="see-also"></a>関連項目

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)

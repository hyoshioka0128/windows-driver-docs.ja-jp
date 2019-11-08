---
title: IRP_MJ_CREATE 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_CREATE 場合は、次の共用体コンポーネントが使用されます。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- IRP_MJ_CREATE ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
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
ms.date: 11/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: c49a6cc4c3551f039961aa39a1dfba3257a63600
ms.sourcegitcommit: 23ca676ade460f8ce7866015559c24728c7c308b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73799190"
---
# <a name="flt_parameters-for-irp_mj_create-union"></a>IRP_MJ_CREATE 共用体の FLT_PARAMETERS

操作の[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_CREATE**](irp-mj-create.md)場合は、次の共用体コンポーネントが使用されます。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIO_SECURITY_CONTEXT     SecurityContext;
    ULONG                    Options;
    USHORT POINTER_ALIGNMENT FileAttributes;
    USHORT                   ShareAccess;
    USHORT POINTER_ALIGNMENT EaLength;
    PVOID                    EaBuffer;
    LARGE_INTEGER            AllocationSize;
  } Create;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>Members

FLT_PARAMETERS の**Create**構造には、次のメンバーが含まれます。

**SecurityContext**

IRP_MJ_CREATE 要求のセキュリティコンテキストを表す[IO_SECURITY_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_security_context)構造体へのポインター。この場合、次のようになります。

- **> SecurityContext AccessState**は、オブジェクトのサブジェクトコンテキスト、アクセスの種類、およびその他の必要なアクセスの種類を含む[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)構造体へのポインターです。

- **> SecurityContext DesiredAccess**は、ファイルに要求されたアクセス権を指定する[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)構造です。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*DesiredAccess*パラメーターを参照してください。

**[オプション]**  
ファイルを作成または開くときに適用するオプション、およびファイルが既に存在する場合に実行するアクションを指定するフラグのビットマスク。 このメンバーの下位24ビットは、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*createoptions*パラメーターに対応しています。 上位8ビットは**Fltcreatefile**の*CreateDisposition*パラメーターに対応します。

**FileAttributes**  
ファイルを作成または開くときに適用される属性のビットマスク。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*fileattributes*パラメーターを参照してください。

**アクセスの許可**  
ファイルに要求された共有アクセス権のビットマスク。 このパラメーターがゼロの場合は、排他アクセスが要求されます。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の "/"*アクセス*パラメーターを参照してください。

**EaLength**  
**EaBuffer**メンバーが指すバッファーの長さ (バイト単位)。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*EaLength*パラメーターを参照してください。

**EaBuffer**  
ファイルに適用される拡張属性 (EA) 情報を格納する、呼び出し元が提供する、 [FILE_FULL_EA_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)構造化されたバッファーへのポインター。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*EaBuffer*パラメーターを参照してください。

**AllocationSize**  
必要に応じて、ファイルの初期割り当てサイズをバイト単位で指定します。 0以外の値は、ファイルが作成、上書き、または置き換えられない限り、無効です。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の割り当て*サイズ*パラメーターを参照してください。

## <a name="remarks"></a>注釈

[IRP_MJ_CREATE](irp-mj-create.md)操作の[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される IRP ベースの**作成**操作のパラメーターが含まれています。 これは[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

IRP_MJ_CREATE は、IRP ベースの操作です。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| Header | *fltkernel .h* (fltkernel. h を含む)

## <a name="see-also"></a>関連項目

[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[FILE_FULL_EA_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[FLT_IS_FASTIO_OPERATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[IRP_MJ_CREATE](irp-mj-create.md)

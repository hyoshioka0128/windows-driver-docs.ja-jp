---
title: IRP_MJ_CREATE_NAMED_PIPE 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_CREATE_NAMED_PIPE 場合は、次の共用体コンポーネントが使用されます。
ms.assetid: cbe7e523-3ae2-424b-a2e2-edaeb64c15c5
keywords:
- IRP_MJ_CREATE_NAMED_PIPE の共用体ファイルシステムドライバーの FLT_PARAMETERS
- FLT_PARAMETERS 共用体ファイルシステムドライバー
- PFLT_PARAMETERS 共用体ポインターファイルシステムドライバー
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
ms.openlocfilehash: dad36c2f94c8a8ce05c993b5a51a161d51a8a91f
ms.sourcegitcommit: 257850d61aa5d1db707dc2f30721319b650e47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801160"
---
# <a name="flt_parameters-for-irp_mj_create_named_pipe-union"></a>IRP_MJ_CREATE_NAMED_PIPE 共用体の FLT_PARAMETERS

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) union 内の次の構造は、 [FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[IRP_MJ_CREATE_NAMED_PIPE](irp-mj-create-named-pipe.md)場合に使用されます。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIO_SECURITY_CONTEXT     SecurityContext;
    ULONG                    Options;
    USHORT POINTER_ALIGNMENT Reserved;
    USHORT                   ShareAccess;
    PVOID                    Parameters;
  } CreatePipe;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>Members

FLT_PARAMETERS の**Createpipe**構造体には、次のメンバーが含まれています。

**SecurityContext**  
IRP_MJ_CREATE_NAMED_PIPE 要求のセキュリティコンテキストを表す[IO_SECURITY_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_security_context)構造体へのポインター。この場合、次のようになります。

- **> SecurityContext AccessState**は、オブジェクトのサブジェクトコンテキスト、アクセスの種類、およびその他の必要なアクセスの種類を含む[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)構造体へのポインターです。

- **> SecurityContext DesiredAccess**は、名前付きパイプに対して要求されるアクセス権を指定する[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)構造です。 詳細については、 [**FltCreateNamedPipeFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatenamedpipefile)の*DesiredAccess*パラメーターを参照してください。

**[オプション]**  
名前付きパイプを作成または開くときに適用されるオプションを指定するフラグのビットマスク。パイプが既に存在する場合に実行されるアクションも指定します。 このメンバーの下位24ビットは、 **FltCreateNamedPipeFile**の*createoptions*パラメーターに対応しています。 上位8ビットは、 **FltCreateNamedPipeFile**の*CreateDisposition*パラメーターに対応します。

**確保**  
確保使用しないでください。

**アクセスの許可**  
名前付きパイプファイルに要求された共有アクセス権のビットマスク。 このパラメーターがゼロの場合は、排他アクセスが要求されます。 詳細については、 [**FltCreateNamedPipeFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatenamedpipefile)への "/"*アクセス*パラメーターの説明を参照してください。

**Parameters**  
作成または開いている名前付きパイプに関する情報を格納している[NAMED_PIPE_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_named_pipe_create_parameters)構造体へのポインター。

## <a name="remarks"></a>注釈

I/o 操作が IRP_MJ_CREATE_NAMED_PIPE 場合、 [FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)には**createpipe**構造体が含まれます。 I/o 操作は[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)構造体によって表されます。操作パラメーターは、コールバックデータの*Iopb*パラメーターが指す[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造内に含まれます。

IRP_MJ_CREATE_NAMED_PIPE 操作のコールバックルーチンが登録されているファイルシステムミニフィルタードライバーは、必要な処理を実行して返す必要があります。

最後の longword フィールド以外は、 **Createpipe**構造体のフィールドが**Create** structure のフィールドと一致している必要があることに注意してください。

IRP_MJ_CREATE_NAMED_PIPE は、IRP ベースの操作です。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| Header| Fltkernel .h (Fltkernel. h を含む) |

## <a name="see-also"></a>関連項目

[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateNamedPipeFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatenamedpipefile)

[IRP_MJ_CREATE_NAMED_PIPE](irp-mj-create-named-pipe.md)

[NAMED_PIPE_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_named_pipe_create_parameters)

---
title: IRP_MJ_CREATE_MAILSLOT 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_CREATE_MAILSLOT 場合は、次の共用体コンポーネントが使用されます。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- IRP_MJ_CREATE_MAILSLOT の共用体ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: f487d320d59d1ec3494922bc5e10a0ade89b6b14
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968339"
---
# <a name="flt_parameters-for-irp_mj_create_mailslot-union"></a>IRP_MJ_CREATE_MAILSLOT 共用体の FLT_PARAMETERS

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) union 内の次の構造は、 [FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[IRP_MJ_CREATE_MAILSLOT](irp-mj-create-mailslot.md)場合に使用されます。

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
  } CreateMailslot;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>メンバー

FLT_PARAMETERS の**Createmailslot**構造には、次のメンバーが含まれています。

**SecurityContext**  
IRP_MJ_CREATE_MAILSLOT 要求のセキュリティコンテキストを表す[IO_SECURITY_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_security_context)構造体へのポインター。この場合、次のようになります。

- **>SecurityContext AccessState**は、オブジェクトのサブジェクトコンテキスト、アクセスの種類、およびその他の必要なアクセスの種類を含む[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)構造体へのポインターです。

- **>SecurityContext DesiredAccess**は、メールスロットに要求されたアクセス権を指定する[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)構造です。 詳細については、 [**FltCreateMailslotFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatemailslotfile)の*DesiredAccess*パラメーターを参照してください。

**[オプション]**  
メールスロットを作成または開くときに適用されるオプションを指定するフラグのビットマスク。また、メールスロットが既に存在する場合に実行されるアクションも指定します。 このメンバーの下位24ビットは、 **FltCreateMailslotFile**の*createoptions*パラメーターに対応しています。 上位8ビットは、 **FltCreateMailslotFile**の*CreateDisposition*パラメーターに対応します。

**予約されています。**  
確保使用しないでください。

**ShareAccess**  
メールスロットファイルに要求された共有アクセス権のビットマスク。 このパラメーターがゼロの場合は、排他アクセスが要求されます。 詳細については、 [**FltCreateMailslotFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatemailslotfile)への "/"*アクセス*パラメーターの説明を参照してください。

**パラメーター**  
作成または開いているメールスロットに関する情報を格納している[MAILSLOT_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters)構造体へのポインター。


## <a name="remarks"></a>注釈

I/o 操作が IRP_MJ_CREATE_MAILSLOT 場合、 [FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)には**createmailslot**構造体が含まれます。 I/o 操作は[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)構造体によって表されます。操作パラメーターは、コールバックデータの*Iopb*パラメーターが指す[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造内に含まれます。

IRP_MJ_CREATE_MAILSLOT 操作のコールバックルーチンが登録されているファイルシステムミニフィルタードライバーは、必要な処理を実行して返す必要があります。

最後の longword フィールド以外に、 **Createmailslot**構造体内のフィールドが**Create** structure のフィールドと一致する必要があることに注意してください。

IRP_MJ_CREATE_MAILSLOT は、IRP ベースの操作です。

## <a name="requirements"></a>要件

**ヘッダー**: fltkernel .H (fltkernel .h を含む)


## <a name="see-also"></a>関連項目

[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[FLT_CALLBACK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateMailslotFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatemailslotfile)

[IRP_MJ_CREATE_MAILSLOT](irp-mj-create-mailslot.md)

[MAILSLOT_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters)


---
title: IRP_MJ_CREATE_MAILSLOT
description: IRP_MJ_CREATE_MAILSLOT
ms.assetid: 6cd04fd0-ee36-421f-8877-f409aba31b17
keywords:
- IRP_MJ_CREATE_MAILSLOT ファイルシステムドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_CREATE_MAILSLOT
api_type:
- NA
ms.date: 11/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 44a0c83a7e6e95f30db7eb99aac75999bdbd995c
ms.sourcegitcommit: 257850d61aa5d1db707dc2f30721319b650e47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801162"
---
# <a name="irp_mj_create_mailslot"></a>IRP_MJ_CREATE_MAILSLOT

## <a name="when-sent"></a>送信時

I/o マネージャーは、新しいメールスロットを作成または開いたときに、IRP_MJ_CREATE_MAILSLOT 要求を送信します。 通常、この IRP は次のように送信されます。

- [**Createmailslot**](https://docs.microsoft.com/windows/win32/api/winbase/nf-winbase-createmailslota)などの Microsoft Win32 関数を呼び出したユーザーモードアプリケーションに代わって。
- または、 [**Iocreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)または[**iocreatefilの場合は、Iodevicethint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)というカーネルモードコンポーネントの代わりに。

メールスロット作成要求が正常に完了した場合、アプリケーションまたはカーネルモードコンポーネントは、メールスロットファイルインスタンスへのハンドルを受け取ります。

IRP_MJ_CREATE_MAILSLOT の処理は[IRP_MJ_CREATE](irp-mj-create.md)とほぼ同じです。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー

ターゲットデバイスオブジェクトがファイルシステムのコントロールデバイスオブジェクトである場合、 *irp > IoStatus. Status*および*irp-> を設定した後に、ファイルシステムドライバーのディスパッチルーチンが irp を完了し、適切な NTSTATUS 値を返す必要があります。IoStatus. 情報*に適切な値を指定します。

それ以外の場合、ファイルシステムドライバーは作成要求を処理する必要があります。

## <a name="operation-file-system-legacy-filter-drivers"></a>操作: ファイルシステムレガシフィルタードライバー

ターゲットデバイスオブジェクトがレガシフィルタードライバーのコントロールデバイスオブジェクトである場合、 *irp > iostatus. Status*と*irp-> を設定した後で、そのドライバーのディスパッチルーチンが irp を完了し、適切な NTSTATUS 値を返す必要があります。IoStatus. 情報*に適切な値を指定します。

それ以外の場合、レガシフィルタードライバーは必要な処理を実行し、フィルターの性質に応じて、IRP を完了するか、スタック上の次の下位のドライバーに渡します。

一般に、レガシフィルタードライバーは、 **IRP_MJ_CREATE_MAILSLOT**への応答として**STATUS_PENDING**を返さないようにする必要があります。 ただし、下位レベルのドライバーから**STATUS_PENDING**が返された場合、レガシフィルタードライバーはこの状態値をドライバーチェーンに渡す必要があります。

## <a name="parameters"></a>パラメーター

ファイルシステムまたはレガシフィルタードライバーは、指定された IRP で[**Iogetlocation entitu**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出して、irp 内の独自の[**スタック位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。 次のパラメーターでは、 *irp*が Irp と*irpsp*をポイントして、IO_STACK_LOCATION を指します。 ドライバーは、create 要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

- *DeviceObject*は、ターゲットデバイスオブジェクトへのポインターです。

- *Irp > フラグ*は、この要求に対して次のフラグに設定されます。
  - IRP_CREATE_OPERATION
  - IRP_DEFER_IO_COMPLETION
  - IRP_SYNCHRONOUS_API

- *Irp > IoStatus*は、最終的な完了状態と要求された操作に関する情報を受け取る[IO_STATUS_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造を指します。 この構造体の**情報**メンバーは、ファイルシステムによって次のいずれかの値に設定されます。
  - FILE_CREATED
  - FILE_OPENED

- *Irp-> irp->requestormode*操作を要求したプロセスの実行モード ( **kernelmode で**または**モード**) を示します。 SL_FORCE_ACCESS_CHECK フラグが設定されている場合、 *> irp->requestormode*が**kernelmode で**の場合でも、アクセスチェックを実行する必要があることに注意してください。

- *Irpsp-> MajorFunction*は IRP_MJ_CREATE_MAILSLOT に設定されます。

- *Irpsp-> フラグ*を SL_FORCE_ACCESS_CHECK に設定できます。 このフラグが設定されている場合は、 *Irp-> irp->requestormode*の値が**kernelmode で**の場合でもアクセスチェックを実行する必要があります。

- *Irpsp-> SecurityContext-> AccessState*は、オブジェクトのサブジェクトコンテキスト、許可されたアクセスの種類、およびその他の必要なアクセスの種類を含む[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)構造体へのポインターです。

- *Irpsp-> Parameters SecurityContext-> DesiredAccess*は、メールスロットに要求されたアクセス権を指定する ACCESS_MASK 構造です。 詳細については、 [**IocreatefilDesiredAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)パラメーターの説明を参照してください。

- *Irpsp-> Parameters. CreateMailslot。オプション*は、メールスロットを作成または開くときに適用されるオプションを指定するフラグのビットマスクです。また、メールスロットが既に存在する場合に実行される操作も指定します。

  このパラメーターの上位8ビットは、 [**Iocreatefil指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)されたデバイス*の処理パラメーターに*対応します。

  このメンバーの下位24ビットは、 *Createoptions*パラメーターに対応して[**iocreatefilを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)指定します。

- *Irpsp-> パラメーター。 CreateMailslot。共有アクセス*は、メールスロットに要求された共有アクセス権のビットマスクです。 このメンバーがゼロの場合は、排他アクセスが要求されます。 詳細については、 [**Iocreatefil指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)している場合は、*このパラメーターの*説明を参照してください。

- *Irpsp-> パラメーター。 CreateMailslot。 parameters*は、メールスロットを作成するときの CREATE パラメーターを含む[MAILSLOT_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters)構造体へのポインターです。

- *Irpsp-> FileObject*は、作成または開くメールスロットを表すために i/o マネージャーによって作成されるファイルオブジェクトへのポインターです。 ファイルシステムが IRP_MJ_CREATE_MAILSLOT 要求を処理すると、このファイルオブジェクトの**Fscontext**と**FsContext2**フィールドが、ファイルシステム固有の値に設定されます。 このため、ファイルシステムによって create 要求が処理されるまで、 **Fscontext**フィールドと**FsContext2**フィールドの値を有効と見なすことはできません。 詳細については、「[ファイルストリーム、ストリームコンテキスト、およびストリームごとのコンテキスト](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts)」を参照してください。

  [**Iocancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen) (および[**fltcancelfileopen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)) は、ファイルオブジェクトの**Flags**フィールドに FO_FILE_OPEN_CANCELLED フラグを設定します。 このフラグを設定すると、IRP_MJ_CREATE_MAILSLOT 要求が取り消され、このファイルオブジェクトに対して[**IRP_MJ_CLOSE**](irp-mj-close.md)要求が発行されることを示します。 作成要求がキャンセルされると、再発行することはできません。

  *Irpsp-> FileObject*パラメーターには、FILE_OBJECT 構造である、関連する**fileobject**フィールドへのポインターが含まれています。 FILE_OBJECT 構造体の関連する**fileobject**フィールドは、既に開いているファイルオブジェクトに対して、特定のメールスロットが開かれていることを示すために使用されます。 これは通常、相対ファイルがディレクトリであることを示していますが、ストリームベースのファイルは、既にファイルのストリームを使用して開いている可能性があります。 FILE_OBJECT 構造体の関連性の**あるフィールドは、IRP_MJ_CREATE_MAILSLOT**の処理中にのみ有効です。

## <a name="see-also"></a>関連項目

[ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[ACCESS_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[FLT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[IRP_MJ_CREATE_MAILSLOT の FLT_PARAMETERS](flt-parameters-for-irp-mj-create-mailslot.md)

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[IO_STACK_LOCATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[IO_STATUS_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocancelfileopen)

[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)

[**Iocreatefilの場合は、デバイスを Ioint にします。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)

[**IoCreateStreamFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobject)

[**Iocreatestreamfileite Tlite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocreatestreamfileobjectlite)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[IRP](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[IRP_MJ_CLEANUP](irp-mj-cleanup.md)

[IRP_MJ_CLOSE](irp-mj-close.md)

[IRP_MJ_CREATE (WDK カーネルリファレンス)](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)

[MAILSLOT_CREATE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mailslot_create_parameters)

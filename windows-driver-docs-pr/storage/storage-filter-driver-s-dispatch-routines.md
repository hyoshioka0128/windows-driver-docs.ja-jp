---
title: 記憶域フィルター ドライバーの Dispatch ルーチン
description: 記憶域フィルター ドライバーの Dispatch ルーチン
ms.assetid: 0d1af035-537f-4632-800b-eb344dc5a3c8
keywords:
- ストレージフィルタードライバー WDK、ディスパッチルーチン
- フィルタードライバー WDK storage、ディスパッチルーチン
- SFD WDK storage、ディスパッチルーチン
- ディスパッチルーチン WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da312423c442c25282d022da3fbc61c6594a38f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844479"
---
# <a name="storage-filter-drivers-dispatch-routines"></a>記憶域フィルター ドライバーの Dispatch ルーチン


## <span id="ddk_storage_filter_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DISPATCH_ROUTINES_KG"></span>


他の上位レベルのカーネルモードドライバーと同様に、ストレージフィルタードライバー (SFD) には、基になるストレージドライバーが*ディスパッチ*エントリポイントを提供するすべての IRP\_MJ\_XXX 要求を処理するための*ディスパッチ*ルーチンが1つ以上必要です. デバイスの性質によっては、SFD の*ディスパッチ*エントリポイントは、特定の要求に対して次のいずれかを実行できます。

-   特別な処理を必要としない要求の場合は、次の下位にあるドライバーの IRP で i/o スタックの場所を設定します。また、場合によっては、 [**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出して、Irp の[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、次の処理のために irp をに渡します。[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用してドライバーを減らします。

-   ストレージクラスドライバーによって既に処理されている要求の場合は、i/o スタックの場所を設定する前に、IRP の i/o スタックの場所の SRB を変更し、場合によっては[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定して、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して irp を次の下位のドライバーに渡します。

-   デバイスの SRB と CDB を含む新しい IRP を設定し、 [**Ioset ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出します。これにより、SRB (およびドライバーが[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)または[**IOBUILDASYNCHRONOUSFSDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を呼び出す場合は Irp) を解放し、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)で IRP を渡すことができます。

    SFD は、多くの場合、新しい Irp を設定します。これは、主要な関数コードの[**irp\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)を使用して行います。

## <a name="span-idprocessing_requestsspanspan-idprocessing_requestsspanspan-idprocessing_requestsspanprocessing-requests"></a><span id="Processing_requests"></span><span id="processing_requests"></span><span id="PROCESSING_REQUESTS"></span>要求の処理


特別な処理を必要としない要求の場合、SFD の*ディスパッチ*ルーチンは通常、入力 IRP を使用して[**IoskipIoCallDriver entilocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、次にクラスドライバーの device オブジェクトと IRP へのポインターを使用して、呼び出しを呼び出します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) SFD は、 *iocompletion*ルーチンの呼び出しが不要で、ドライバーのデバイスの i/o スループットが低下するため、特別な処理を必要としない Irp で[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定することはめったにありません。 SFD で Iocompletion ルーチンが設定されている場合は、 **IoskipIoCallDriver**を呼び出す前に[**iocopy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)を呼び出し、 [**iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出します。

特別な処理を必要とする要求の場合、SFD は次のことを実行できます。

1.  [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)、 [**ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)、または[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)を使用して新しい IRP を作成します。通常は、それ自体の i/o スタックの場所を指定します。

2.  IRP を割り当てることができなかった場合は、返された IRP ポインターの**NULL**および戻り値 **\_\_リソースが不足**していることを確認してください。

3.  ドライバーによって作成された IRP に SFD の i/o スタックの場所が含まれている場合は、 [**Iosetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetnextirpstacklocation)ドの場所を呼び出して、IRP スタックの場所ポインターを設定します。 次に、 [**Ioget"enti"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出して、ドライバーによって作成された IRP 内の専用 i/o スタックの場所へのポインターを取得し、独自の[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンで使用する状態を設定します。

4.  [**IogetnextiMJ Stacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)を呼び出して、ドライバーによって作成された irp 内の次の下位にあるドライバーの i/o スタックの場所へのポインターを取得し、主要な関数コードの**IRP\_\_SCSI**と SRB (「[ストレージクラスドライバー](storage-class-drivers.md)」を参照) を使用して設定します。

5.  必要に応じて、デバイスに転送されるデータをデバイス固有の非標準形式に変換します。

6.  ドライバーが、 [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)または[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)の呼び出しを使用して SRB、SCSI 要求-sense buffer、MDL、または IRP のメモリなどのメモリを割り当てた場合、またはドライバーを変換する必要がある場合は、 [**ioset ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出します。デバイス固有の非標準形式でデバイスから転送されるデータ。

7.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、ドライバーによって作成された IRP を次の下位のドライバーに渡します。

## <a name="span-idhandling_srb_formatsspanspan-idhandling_srb_formatsspanspan-idhandling_srb_formatsspanhandling-srb-formats"></a><span id="Handling_SRB_formats"></span><span id="handling_srb_formats"></span><span id="HANDLING_SRB_FORMATS"></span>SRB 形式の処理


Windows 8 以降では、クラスドライバーとポートドライバーの間の SFD フィルター処理で、サポートされている SRB 形式を確認する必要があります。 具体的には、SRB 形式を検出し、構造体のメンバーに正しくアクセスする必要があります。 IRP の SRB は、 [**SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)、または[**ストレージ\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_storage_request_block)のいずれかです。 フィルタードライバーは、以下のポートドライバーで SRBs がサポートされているかどうかを事前に判断できます。そのためには、 [**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)要求を発行し、 **storageadapterproperty**識別子を指定します。 [**ストレージ\_アダプターの\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)構造体で返される**Srbtype**と**AddressType**の値は、ポートドライバーで使用される SRB 形式とアドレス指定スキームを示します。 フィルタードライバーによって割り当てられて送信される新しい SRBs は、クエリによって返される型である必要があります。

同様に、Windows 8 以降では、 [**SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)の種類の SRBs のみをサポートする SFDs は、[**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)構造体で返された**srbtype**値がに設定されていることを確認する必要があります。**SRB\_TYPE\_SCSI\_要求\_ブロック**です。 **Srbtype**が SRB に設定されている場合は、代わりに**ストレージ\_要求\_ブロックを入力**すると、フィルタードライバーは[**IOCTL\_storage\_QUERY の完了ルーチンを設定する必要があり\_を処理\_\_このプロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)は、上のドライバーによって送信された要求で**storageadapterproperty**識別子が設定されている場合に設定されます。 完了ルーチンでは、**ストレージ\_アダプターの\_記述子**の**srbtype**メンバーが、サポートされている型を正しく設定するために、 **SCSI\_要求\_ブロックの SRB\_\_型**に変更されます。

次に、両方の SRB 形式を処理するフィルターディスパッチルーチンの例を示します。

```ManagedCPlusPlus
NTSTATUS FilterScsiIrp(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp
    )
{
    PFILTER_DEVICE_EXTENSION  deviceExtension = DeviceObject->DeviceExtension;
    PIO_STACK_LOCATION irpStack = IoGetCurrentIrpStackLocation(Irp);
    NTSTATUS status;
    PSCSI_REQUEST_BLOCK srb;   
    ULONG srbFunction;
    ULONG srbFlags;

    //
    // Acquire the remove lock so that device will not be removed while
    // processing this irp.
    //

    status = IoAcquireRemoveLock(&deviceExtension->RemoveLock, Irp);

    if (!NT_SUCCESS(status)) {
        Irp->IoStatus.Status = status;
        IoCompleteRequest(Irp, IO_NO_INCREMENT);
        return status;
    }

    srb = irpStack->Parameters.Scsi.Srb;
     
    if (srb->Function == SRB_FUNCTION_STORAGE_REQUEST_BLOCK) {
        srbFunction = ((PSTORAGE_REQUEST_BLOCK)srb)->SrbFunction;
        srbFlags = ((PSTORAGE_REQUEST_BLOCK)srb)->SrbFlags;
    } else {
        srbFunction = srb->Function;
        srbFlags = srb->SrbFlags;
    }

    if (srbFunction == SRB_FUNCTION_EXECUTE_SCSI) {
        if (srbFlags & SRB_FLAGS_UNSPECIFIED_DIRECTION) {
            // ...

            // filter processing for SRB_FUNCTION_EXECUTE_SCSI

            // ...
        }
    }

    IoMarkIrpPending(Irp);
    IoCopyCurrentIrpStackLocationToNext(Irp);
    IoSetCompletionRoutine(Irp,
                           FilterScsiIrpCompletion,
                           DeviceExtension->DeviceObject,
                           TRUE, TRUE, TRUE);
    IoCallDriver(DeviceExtension->TargetDeviceObject, Irp);

    return STATUS_PENDING; 
}
```

## <a name="span-idsetting_up_requestsspanspan-idsetting_up_requestsspanspan-idsetting_up_requestsspansetting-up-requests"></a><span id="Setting_up_requests"></span><span id="setting_up_requests"></span><span id="SETTING_UP_REQUESTS"></span>要求の設定


ストレージクラスドライバーと同様に、SFD は、ドライバーの*ディスパッチ*ルーチンから呼び出される*Buildrequest*または*splittransferrequest*ルーチンを持つことができます。また、同じ機能をインラインで実装する場合もあります。

*Buildrequest*ルーチンと*splittransferrequest*ルーチンの詳細については、「[ストレージクラスドライバー](storage-class-drivers.md)」を参照してください。 *ディスパッチ*ルーチンの一般的な要件の詳細については、「[ディスパッチルーチンの記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)」を参照してください。

 

 





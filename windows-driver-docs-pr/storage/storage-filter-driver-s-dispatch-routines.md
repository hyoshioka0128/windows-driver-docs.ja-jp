---
title: 記憶域フィルター ドライバーの Dispatch ルーチン
description: 記憶域フィルター ドライバーの Dispatch ルーチン
ms.assetid: 0d1af035-537f-4632-800b-eb344dc5a3c8
keywords:
- 記憶域フィルター ドライバー WDK、ディスパッチ ルーチン
- フィルター ドライバー WDK の記憶域、ルーチンのディスパッチ
- SFD WDK ストレージ、ディスパッチ ルーチン
- ディスパッチ ルーチン WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78855318fcb20d5d6a25166cd49712c03d8b83b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370432"
---
# <a name="storage-filter-drivers-dispatch-routines"></a>記憶域フィルター ドライバーの Dispatch ルーチン


## <span id="ddk_storage_filter_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DISPATCH_ROUTINES_KG"></span>


他の高度なカーネル モード ドライバーと同様、記憶域フィルター ドライバー (SFD) を 1 つ以上が必要*ディスパッチ*すべて IRP を処理するルーチン\_MJ\_XXX 要求を基になる記憶域ドライバー提供、*ディスパッチ*エントリ ポイント。 そのデバイスの性質によって、*ディスパッチ*SFD のエントリ ポイントは、特定の要求は、次のいずれかを行う可能性があります。

-   次の下位ドライバー用の IRP で I/O スタックの場所を設定して、特別な処理を必要としない要求を呼び出す可能性[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)を設定するその[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP、およびパスの下位のドライバーによってさらに処理の IRP の日常的な[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

-   I/O スタックの場所をセットアップする前に IRP の I/O スタックの場所で SRB を変更する記憶域クラス ドライバーによって既に処理要求の場合、必要に応じて設定を[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンと IRP のパス使用してドライバーを次の下位に[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

-   新しいセットアップ SRB とそのデバイスでは、CDB IRP を呼び出す[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)ため、SRB (とドライバーを呼び出す場合の IRP [ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)または[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)) を解放し、上で IRP を渡す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

    主要な関数コードで新しい Irp を設定する最も可能性があります、SFD [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)します。

## <a name="span-idprocessingrequestsspanspan-idprocessingrequestsspanspan-idprocessingrequestsspanprocessing-requests"></a><span id="Processing_requests"></span><span id="processing_requests"></span><span id="PROCESSING_REQUESTS"></span>要求の処理


特別な処理を必要としない要求を*ディスパッチ*、SFD のルーチンを呼び出す通常[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) IRP を入力し、呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)クラス ドライバーのデバイス オブジェクトと IRP へのポインター。 SFD のほとんどの設定に注意してください、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ため、特別な処理が不要な Irp のルーチンへの呼び出し、 *IoCompletion*ルーチンが必要ないとドライバーのデバイスの I/O スループットが低下します。 設定することは、SFD 場合、 *IoCompletion*ルーチンを呼び出す[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)の代わりに**IoSkipCurrentIrpStackLocation**号餧ェヒェマル[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)呼び出す前に**保留**します。

特別な処理を必要と要求の場合、SFD は、次の操作を行うことができます。

1.  作成と新しい IRP [ **IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)、 [ **IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)、 [ **IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)、または[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)、通常は自身の I/O スタックの場所を指定します。

2.  確認の返された IRP ポインター **NULL**戻って**状態\_不十分\_リソース**IRP を割り当てられていない場合。

3.  IRP がドライバー作成では、SFD の I/O スタックの場所が含まれている場合は、呼び出す[ **IoSetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetnextirpstacklocation) IRP スタックの場所のポインターを設定します。 次に呼び出す[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation) IRP がドライバー作成では、独自 I/O スタックの場所にポインターを取得し、それ自体で使用される状態を使用してのことを設定する[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン。

4.  呼び出す[ **IoGetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation) IRP がドライバー作成で、次の下位ドライバーの I/O スタックの場所へのポインターを取得し、主要な関数のコードを設定して**IRP\_MJ\_SCSI**と、SRB (を参照してください[ストレージ クラス ドライバー](storage-class-drivers.md))。

5.  必要に応じて、デバイスに固有の非標準形式に、デバイスに転送されるデータを変換します。

6.  呼び出す[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)ドライバーへの呼び出しで、SRB、SCSI 要求センス バッファー、MDL、または IRP のメモリなど、任意のメモリを割り当てられた場合[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)または[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)特定のデバイス、非標準の形式でデバイスから転送されるかどうか、ドライバーは、データを変換する必要がありますか。

7.  ドライバーが作成した IRP (および使用) を渡すと、次の下位ドライバー [**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

## <a name="span-idhandlingsrbformatsspanspan-idhandlingsrbformatsspanspan-idhandlingsrbformatsspanhandling-srb-formats"></a><span id="Handling_SRB_formats"></span><span id="handling_srb_formats"></span><span id="HANDLING_SRB_FORMATS"></span>書式設定 SRB の処理


Windows 8 以降、クラス ドライバーとポートのドライバーのフィルター処理、SFD は、サポートされる SRB 形式のチェックする必要があります。 具体的には、これは、SRB 形式を検出し、構造体のメンバーを適切にアクセスする必要があります。 IRP で SRB がいずれか、 [ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)とまたは[**ストレージ\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_storage_request_block). フィルター ドライバーを事前に決定できるどのされる Srb が発行することにより、ポートのドライバーでサポートされて、 [ **IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)要求指定して、 **StorageAdapterProperty**識別子。 **SrbType**と**AddressType**に返される値、 [**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)構造体は、SRB 形式とポート ドライバーによって使用されるアドレス スキームを示します。 新しいされる Srb 割り当てられ、フィルター ドライバーによって送信されたクエリによって返される型でなければなりません。

同様に、Windows 8 以降、SFDs のされる Srb のみをサポートしている、 [ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)型は、ことを確認する必要があります、 **SrbType**返された値、 [**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)構造に設定されている**SRB\_型\_SCSI\_要求\_ブロック**します。 状況を処理するときに**SrbType**に設定されている**SRB\_型\_ストレージ\_要求\_ブロック**代わりに、フィルター ドライバーを設定する必要があります、完了ルーチンの[ **IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)ときに、 **StorageAdapterProperty**その上ドライバーによって送信された要求の識別子を設定します。 入力候補のルーチンで、 **SrbType**内のメンバー、**ストレージ\_アダプター\_記述子**するように変更**SRB\_型\_SCSI\_要求\_ブロック**を正しくサポートされている型を設定します。

次は、両方の SRB 形式を処理するフィルター ディスパッチ ルーチンの例です。

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

## <a name="span-idsettinguprequestsspanspan-idsettinguprequestsspanspan-idsettinguprequestsspansetting-up-requests"></a><span id="Setting_up_requests"></span><span id="setting_up_requests"></span><span id="SETTING_UP_REQUESTS"></span>要求の設定


SFD 可能性がありますが、記憶域クラス ドライバーなど*BuildRequest*または*SplitTransferRequest*ドライバーから呼び出されるルーチンを*ディスパッチ*ルーチン、または実装があります同じ機能インラインです。

詳細については*BuildRequest*と*SplitTransferRequest*ルーチンを参照してください[ストレージ クラス ドライバー](storage-class-drivers.md)します。 一般的な要件の詳細については*ディスパッチ*ルーチンを参照してください[書き込みディスパッチ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)します。

 

 





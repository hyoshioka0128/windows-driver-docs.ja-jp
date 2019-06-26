---
title: SendDownStreamIrp 関数
description: SendDownStreamIrp 関数
ms.assetid: 09a06041-5b26-4796-b9b8-d7d27321d955
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbd6f1c6b52ffd88cbd46f82c791b83452b8d5f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355809"
---
# <a name="senddownstreamirp-function"></a>SendDownStreamIrp 関数


コード例を`SendDownStreamIrp`このトピックで提供されている関数は、ACPI ドライバーを同期 IOCTL 要求を送信するドライバーによって提供される関数を実装する方法を示します。 `SendDownStreamIrp`関数は、送信に使用できる、 [ **IOCTL\_ACPI\_EVAL\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)要求、 [ **IOCTL\_ACPI\_EVAL\_メソッド\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)要求、または[ **IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求。

コードの使用例、`SendDownStreamIrp`このセクションに記載されている関数は、次の一連の操作を実行します。

-   イベント オブジェクトを作成します。

-   呼び出し[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest) IOCTL 要求を作成します。

-   呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IOCTL 要求を送信します。

-   ACPI のドライバーが、要求が完了したことを示すイベント オブジェクトに通知するまで待機します。

-   呼び出し元に、要求の状態を返します。

```cpp
NTSTATUS
SendDownStreamIrp(
    IN PDEVICE_OBJECT   Pdo,
    IN ULONG            Ioctl,
    IN PVOID            InputBuffer,
    IN ULONG            InputSize,
    IN PVOID            OutputBuffer,
    IN ULONG            OutputSize
)
/*
Routine Description:
    General-purpose function called to send a request to the PDO. 
    The IOCTL argument accepts the control method being passed down
    by the calling function

    This subroutine is only valid for the IOCTLS other than ASYNC EVAL. 

Parameters:
    Pdo             - the request is sent to this device object
    Ioctl           - the request - specified by the calling function
    InputBuffer     - incoming request
    InputSize       - size of the incoming request
    OutputBuffer    - the answer
    OutputSize      - size of the answer buffer

Return Value:
    NT Status of the operation
*/
{
    IO_STATUS_BLOCK     ioBlock;
    KEVENT              myIoctlEvent;
    NTSTATUS            status;
    PIRP                irp;

    // Initialize an event to wait on
    KeInitializeEvent(&myIoctlEvent, SynchronizationEvent, FALSE);

    // Build the request
    irp = IoBuildDeviceIoControlRequest(
        Ioctl, 
        Pdo,
        InputBuffer,
        InputSize,
        OutputBuffer,
        OutputSize,
        FALSE,
        &myIoctlEvent,
        &ioBlock);

    if (!irp) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    // Pass request to Pdo, always wait for completion routine
    status = IoCallDriver(Pdo, irp);

    if (status == STATUS_PENDING) {
        // Wait for the IRP to be completed, and then return the status code
        KeWaitForSingleObject(
            &myIoctlEvent,
            Executive,
            KernelMode,
            FALSE,
            NULL);

        status = ioBlock.Status;
    }

    return status;
}
```

 

 





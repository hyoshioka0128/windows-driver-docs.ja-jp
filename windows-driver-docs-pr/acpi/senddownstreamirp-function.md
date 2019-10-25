---
title: SendDownStreamIrp 関数
description: SendDownStreamIrp 関数
ms.assetid: 09a06041-5b26-4796-b9b8-d7d27321d955
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 899f65d78d2e4b05a8eba84d44e082b1f75c9b17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831467"
---
# <a name="senddownstreamirp-function"></a>SendDownStreamIrp 関数


このトピックで提供する `SendDownStreamIrp` 関数のコード例では、同期 IOCTL 要求を ACPI ドライバーに送信するドライバーによって提供される関数を実装する方法を示します。 `SendDownStreamIrp` 関数を使用すると、 [**acpi\_eval\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)要求、 [**ioctl\_acpi\_eval\_method\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)要求、または[**ioctl\_acpi\_ENUM\_を送信できます。子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求を\_します。

このセクションに含まれる `SendDownStreamIrp` 関数のコード例では、次の一連の操作を実行します。

-   イベントオブジェクトを作成します。

-   [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出して、IOCTL 要求を作成します。

-   [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、IOCTL 要求を送信します。

-   は、ACPI ドライバーがイベントオブジェクトを通知するまで待機します。これは、要求が完了したことを示します。

-   要求の状態を呼び出し元に返します。

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

 

 





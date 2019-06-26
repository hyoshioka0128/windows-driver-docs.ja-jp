---
title: IRQL PASSIVE_LEVEL にデバイスの構成情報の取得
description: IRQL PASSIVE_LEVEL にデバイスの構成情報の取得
ms.assetid: 672fb3d8-6e64-425b-a035-8f8ecfd624f1
keywords:
- デバイス構成領域、I/O の WDK カーネル
- デバイス構成領域 WDK I/O
- 構成領域 WDK I/O
- WDK の I/O の領域
- PASSIVE_LEVEL WDK
- ドライバー スタック WDK 構成情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df25c490a2d5145a65ba8b5bab1a3d8ca134fb47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384931"
---
# <a name="obtaining-device-configuration-information-at-irql--passivelevel"></a>IRQL でデバイスの構成情報を取得するパッシブ =\_レベル





IRQL でアクセスのデバイス構成領域にパッシブ =\_レベルが使用する必要があります[ **IRP\_MN\_読み取り\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)と[ **IRP\_MN\_書き込み\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)します。 IRP スタックの指定の構成領域にアクセスして、I/O バッファーがします。 説明を参照して、 [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)詳細については、構造体。

次のコード サンプルでは、デバイスの構成の領域にアクセスする方法を示します。

```cpp
NTSTATUS
ReadWriteConfigSpace(
    IN PDEVICE_OBJECT  DeviceObject,
    IN ULONG  ReadOrWrite,  // 0 for read, 1 for write
    IN PVOID  Buffer,
    IN ULONG  Offset,
    IN ULONG  Length
    )
{
    KEVENT event;
    NTSTATUS status;
    PIRP irp;
    IO_STATUS_BLOCK ioStatusBlock;
    PIO_STACK_LOCATION irpStack;
    PDEVICE_OBJECT targetObject;

    PAGED_CODE();
    KeInitializeEvent(&event, NotificationEvent, FALSE);
    targetObject = IoGetAttachedDeviceReference(DeviceObject);
    irp = IoBuildSynchronousFsdRequest(IRP_MJ_PNP,
                                       targetObject,
                                       NULL,
                                       0,
                                       NULL,
                                       &event,
                                       &ioStatusBlock);
    if (irp == NULL) {
        status = STATUS_INSUFFICIENT_RESOURCES;
        goto End;
    }
    irpStack = IoGetNextIrpStackLocation(irp);
    if (ReadOrWrite == 0) {
        irpStack->MinorFunction = IRP_MN_READ_CONFIG;
    } else {
        irpStack->MinorFunction = IRP_MN_WRITE_CONFIG;
    }
    irpStack->Parameters.ReadWriteConfig.WhichSpace = PCI_WHICHSPACE_CONFIG;
    irpStack->Parameters.ReadWriteConfig.Buffer = Buffer;
    irpStack->Parameters.ReadWriteConfig.Offset = Offset;
    irpStack->Parameters.ReadWriteConfig.Length = Length;

    // Initialize the status to error in case the bus driver does not 
    // set it correctly.
    irp->IoStatus.Status = STATUS_NOT_SUPPORTED;
    status = IoCallDriver(targetObject, irp);
    if (status == STATUS_PENDING) {
        KeWaitForSingleObject(&event, Executive, KernelMode, FALSE, NULL);
        status = ioStatusBlock.Status;
    }
End:
    // Done with reference
    ObDereferenceObject(targetObject);
    return status;
}
```

 

 





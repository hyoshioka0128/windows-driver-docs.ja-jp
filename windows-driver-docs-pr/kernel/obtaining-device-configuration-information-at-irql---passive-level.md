---
title: IRQL PASSIVE_LEVEL でのデバイス構成情報の取得
description: IRQL PASSIVE_LEVEL でのデバイス構成情報の取得
ms.assetid: 672fb3d8-6e64-425b-a035-8f8ecfd624f1
keywords:
- I/o WDK カーネル、デバイス構成領域
- デバイス構成領域 WDK i/o
- 構成領域の WDK i/o
- 領域 WDK i/o
- PASSIVE_LEVEL WDK
- ドライバースタック WDK の構成情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cebb5529949268dd829db22c20b9e77a88ff348f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827747"
---
# <a name="obtaining-device-configuration-information-at-irql--passive_level"></a>IRQL = パッシブ\_レベルでのデバイス構成情報の取得





IRQL = パッシブ\_レベルでデバイスの構成領域にアクセスするには、Irp を使用する必要があります。 [ **\_\_読み取り\_config**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)と[**irp\_\_書き込み\_構成を書き込む**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)必要があります。 IRP スタックで、アクセスする構成領域と i/o バッファーの場所を指定します。 詳細については、 [**IO\_STACK\_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体の説明を参照してください。

次のコードサンプルは、デバイスの構成領域にアクセスする方法を示しています。

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

 

 





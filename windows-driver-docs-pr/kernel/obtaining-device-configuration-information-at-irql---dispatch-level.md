---
title: IRQL DISPATCH_LEVEL でのデバイス構成情報の取得
description: IRQL DISPATCH_LEVEL でのデバイス構成情報の取得
ms.assetid: e168a12b-f32e-4b8d-8768-dc622b37b421
keywords:
- I/o WDK カーネル、デバイス構成領域
- デバイス構成領域 WDK i/o
- 構成領域の WDK i/o
- 領域 WDK i/o
- DISPATCH_LEVEL WDK
- BUS_INTERFACE_STANDARD
- ドライバースタック WDK の構成情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663a95a63cf648c523d19375f1bcc2441b5654af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827760"
---
# <a name="obtaining-device-configuration-information-at-irql--dispatch_level"></a>IRQL = ディスパッチ\_レベルでのデバイス構成情報の取得





「 [Irql = パッシブ\_レベルでのデバイス構成情報の取得](obtaining-device-configuration-information-at-irql---passive-level.md)」で説明されている方法では、i/o 要求パケット (irp) を使用します。そのため、IRQL = パッシブ\_レベルで実行されているドライバーにのみ有効です。 IRQL = ディスパッチ\_レベルで実行されているドライバーは、バスインターフェイスを使用してデバイス構成領域データを取得する必要があります。 このデータを取得するには、バス固有のインターフェイス、またはシステムによって提供されるバスに依存しないバスインターフェイス、**バス\_インターフェイス\_標準**を使用できます。

GUID_BUS_INTERFACE_STANDARD インターフェイス (`wdmguid.h`で定義) を使用すると、デバイスドライバーは、バスドライバーとの通信に i/o 要求パケット (IRP) を使用するのではなく、親バスドライバールーチンを直接呼び出すことができます。 特に、このインターフェイスを使用すると、ドライバーは次の機能に対してバスドライバーが提供するルーチンにアクセスできます。

-    バスアドレスの変換 
-    バスアダプターが DMA をサポートしている場合の DMA アダプター構造の取得 
-    バス上の特定のデバイスのバス構成領域の読み取りと設定 

このインターフェイスを使用するには、InterfaceType = GUID_BUS_INTERFACE_STANDARD を使用して、バスドライバーに IRP_MN_QUERY_INTERFACE IRP を送信します。 バスドライバーは、インターフェイスの個々のルーチンへのポインターを含む BUS_INTERFACE_STANDARD 構造体へのポインターを提供します。


可能であれば、bus **\_interface\_standard**を使用することをお勧めします。 BUS **\_interface\_standard**を使用している場合、バス番号は構成情報を取得する必要がないため、ドライバーは頻繁に使用する必要があります。バス固有のインターフェイスを取得するときに、バス番号を特定します。 PCI など、一部のバスのバス番号は動的に変更されます。 そのため、ドライバーは PCI ポートに直接アクセスするためにバス番号に依存しないようにする必要があります。 これにより、システム障害が発生する可能性があります。

IRQL = ディスパッチ\_レベルで PCI デバイスの構成領域にアクセスするには、次の3つの手順を実行する必要があります。

1.  \_IRP = パッシブ\_レベルで[ **\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求を送信して、PCI バスドライバーから直接呼び出しインターフェイス構造 (**BUS\_interface\_STANDARD**) を取得します。 これを非ページプールメモリ (通常はデバイス拡張機能) に格納します。

2.  **バス\_インターフェイス\_標準**インターフェイスルーチン、 [*setbusdata*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/gg604856(v=vs.85)) 、および[*GETBUSDATA*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_set_device_data)を呼び出して、IRQL = DISPATCH\_レベルで PCI 構成領域にアクセスします。

3.  インターフェイスを逆参照します。 PCI バスドライバーは、を返す前にインターフェイスの参照カウントを取得するため、インターフェイスにアクセスするドライバーは、不要になった時点で逆参照する必要があります。

次のコードサンプルは、これら3つの手順を実装する方法を示しています。

```cpp
NTSTATUS
GetPCIBusInterfaceStandard(
    IN  PDEVICE_OBJECT DeviceObject,
    OUT PBUS_INTERFACE_STANDARD BusInterfaceStandard
    )
/*++
Routine Description:
    This routine gets the bus interface standard information from the PDO.
Arguments:
    DeviceObject - Device object to query for this information.
    BusInterface - Supplies a pointer to the retrieved information.
Return Value:
    NT status.
--*/ 
{
    KEVENT event;
    NTSTATUS status;
    PIRP irp;
    IO_STATUS_BLOCK ioStatusBlock;
    PIO_STACK_LOCATION irpStack;
    PDEVICE_OBJECT targetObject;

    Bus_KdPrint(("GetPciBusInterfaceStandard entered.\n"));
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
    irpStack = IoGetNextIrpStackLocation( irp );
    irpStack->MinorFunction = IRP_MN_QUERY_INTERFACE;
    irpStack->Parameters.QueryInterface.InterfaceType = (LPGUID)&GUID_BUS_INTERFACE_STANDARD;
    irpStack->Parameters.QueryInterface.Size = sizeof(BUS_INTERFACE_STANDARD);
    irpStack->Parameters.QueryInterface.Version = 1;
    irpStack->Parameters.QueryInterface.Interface = (PINTERFACE)BusInterfaceStandard;
    irpStack->Parameters.QueryInterface.InterfaceSpecificData = NULL;

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

次のコードスニペットは、 [*Getbusdata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_set_device_data)インターフェイスルーチンを使用して構成領域データを取得する方法を示しています (手順 2)。

```cpp
 bytes = busInterfaceStandard.GetBusData(
                    busInterfaceStandard.Context,
                    PCI_WHICHSPACE_CONFIG,
                    Buffer
                    Offset,
                    Length);
```

インターフェイスを使用してドライバーを実行すると、次のスニペットのようなコードを使用してインターフェイスを逆参照できます (ステップ 3)。 インターフェイスを逆参照した後、ドライバーがインターフェイスルーチンを呼び出すことはできません。

```cpp
    (busInterfaceStandard.InterfaceDereference)(
                    (PVOID)busInterfaceStandard.Context);
```

インターフェイスは、PCI バスドライバーのアクセスを使用して、バスハードウェアへの呼び出し元のアクセスを同期します。 ドライバーライターは、バスハードウェアにアクセスするために PCI バスドライバーとの競合を避けるために、スピンロックの作成について心配する必要はありません。

必要なのは、バス、関数、デバイスの番号だけであれば、通常はバスインターフェイスを利用してこの情報を取得する必要がないことに注意してください。 ターゲットデバイスの PDO を[**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)関数に渡すことで、このデータを間接的に取得できます。次に例を示します。

```cpp
    ULONG   propertyAddress, length;
    USHORT  FunctionNumber, DeviceNumber;

    // Get the BusNumber. Be warned that bus numbers may be
    // dynamic and therefore subject to change unpredictably!!!
    IoGetDeviceProperty(PhysicalDeviceObject,
                        DevicePropertyBusNumber,
                        sizeof(ULONG),
                        (PVOID)&BusNumber,
                        &length);

    // Get the DevicePropertyAddress
    IoGetDeviceProperty(PhysicalDeviceObject,
                        DevicePropertyAddress,
                        sizeof(ULONG),
                        (PVOID)&propertyAddress,
                        &length);

    // For PCI, the DevicePropertyAddress has device number 
    // in the high word and the function number in the low word. 
    FunctionNumber = (USHORT)((propertyAddress) & 0x0000FFFF);
    DeviceNumber = (USHORT)(((propertyAddress) >> 16) & 0x0000FFFF);
```

 

 





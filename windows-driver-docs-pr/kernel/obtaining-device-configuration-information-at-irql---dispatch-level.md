---
title: IRQL DISPATCH_LEVEL にデバイスの構成情報の取得
description: IRQL DISPATCH_LEVEL にデバイスの構成情報の取得
ms.assetid: e168a12b-f32e-4b8d-8768-dc622b37b421
keywords:
- デバイス構成領域、I/O の WDK カーネル
- デバイス構成領域 WDK I/O
- 構成領域 WDK I/O
- WDK の I/O の領域
- DISPATCH_LEVEL WDK
- BUS_INTERFACE_STANDARD
- ドライバー スタック WDK 構成情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c6001a6fbba75975a9d1528abf7e530b67898c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384939"
---
# <a name="obtaining-device-configuration-information-at-irql--dispatchlevel"></a>IRQL でデバイスの構成情報を取得するディスパッチ =\_レベル





メソッドに、 [IRQL でデバイスの構成情報を取得するパッシブ =\_レベル](obtaining-device-configuration-information-at-irql---passive-level.md)セクションでは、I/O の使用により、要求パケット (Irp) であるため、IRQL で実行されているドライバーの有効なのみパッシブを=\_レベルです。 IRQL で実行されているドライバーのディスパッチを =\_レベルは、バス インターフェイスを使用してデバイスの構成領域のデータを取得する必要があります。 このデータを取得するには、bus 固有のインターフェイスまたはシステム提供のバスに依存しないバス インターフェイスを使用できます**BUS\_インターフェイス\_標準**します。

GUID_BUS_INTERFACE_STANDARD インターフェイス (で定義されている`wdmguids.h`) により、デバイス ドライバーのバス ドライバーと通信する I/O 要求パケット (IRP) を使用する代わりに親バス ドライバーのルーチンへの直接の呼び出しを行います。 具体的には、このインターフェイスでは、ドライバー、バス ドライバーは、次の関数を提供するルーチンへのアクセスを有効にします。

-    バスのアドレスに変換 
-    バス アダプターが DMA をサポートしている場合、DMA アダプターの構造を取得します。 
-    読み取りおよびバス上の特定のデバイスのバスの構成領域の設定 

このインターフェイスを使用するには、InterfaceType にバス ドライバーに IRP_MN_QUERY_INTERFACE IRP を送信 GUID_BUS_INTERFACE_STANDARD を = です。 バス ドライバーでは、インターフェイスの個々 のルーチンへのポインターを格納する BUS_INTERFACE_STANDARD 構造体へのポインターを提供します。


使用することをお勧め**BUS\_インターフェイス\_標準**バス番号を使用する場合は、構成情報を取得する必要はないため、可能な限り**BUS\_インターフェイス\_標準**バスに固有のインターフェイスを取得するときに、ドライバーはバス番号を識別多くの場合する必要があります。 PCI などのいくつかのバスのバス番号が動的に変更できます。 そのため、ドライバーでは、PCI ポートに直接アクセスするバス番号に依存する必要があります。 これは、システム障害に生じる可能性があります。

IRQL で PCI デバイスの構成領域にアクセスするときに、3 つの手順が必要なディスパッチを =\_レベル。

1.  送信、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IRQL で要求 = パッシブ\_ダイレクト呼び出しインターフェイス構造体を取得するレベル (**BUS\_インターフェイス\_標準**)、PCI バス ドライバーから。 この操作を (通常はデバイスの拡張機能) での非ページ プール メモリに格納します。

2.  呼び出す、 **BUS\_インターフェイス\_標準**インターフェイスのルーチン、 [ *SetBusData* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/gg604856(v=vs.85))と[ *GetBusData* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-get_set_device_data)IRQL で PCI 構成領域にアクセスするには、ディスパッチ =\_レベル。

3.  インターフェイスを逆参照します。 PCI バス ドライバーは、参照カウントをインターフェイスに返す前に、ドライバー、インターフェイスにアクセスする必要がありますそれを逆参照、不要になった後、されます。

次のコード サンプルでは、これら 3 つの手順を実装する方法を示しています。

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

次のコード スニペットを使用する方法を示しています、 [ *GetBusData* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-get_set_device_data)インターフェイスの構成の空間データ (ステップ 2) を取得するルーチン。

```cpp
 bytes = busInterfaceStandard.GetBusData(
                    busInterfaceStandard.Context,
                    PCI_WHICHSPACE_CONFIG,
                    Buffer
                    Offset,
                    Length);
```

インターフェイスと、ドライバーが完了すると (ステップ 3) インターフェイスを逆参照するのに次のスニペットのようなコードを使用できます。 ドライバーは、インターフェイスを逆参照した後はインターフェイスのルーチンを呼び出す必要がありますされません。

```cpp
    (busInterfaceStandard.InterfaceDereference)(
                    (PVOID)busInterfaceStandard.Context);
```

インターフェイスは、PCI バス ドライバーのアクセス権を持つバス ハードウェアへの呼び出し元のアクセスを同期します。 ドライバーのライターにバス ハードウェアにアクセスするため、PCI バス ドライバーを使用した競合を回避するために、スピン ロックの作成について入力する必要はありません。

バス、関数、およびデバイスの番号をすべての必要な場合必要はありません、通常、この情報を取得するバスのインターフェイスに頼るに注意してください。 このデータを取得できるない直接にターゲット デバイスの PDO を渡すことによって、 [ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)次のように機能します。

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

 

 





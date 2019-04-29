---
title: HF デバイスの Bluetooth のアドレスの取得
description: HF デバイス トピックの取得の Bluetooth アドレスは、オーディオ ドライバーがハンズフリー (HF) のペアになっているデバイスの Bluetooth のアドレスを取得する方法について説明します。
ms.assetid: A3A33459-869A-4F75-B1B9-A3D59863E82C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87fd8e14ec3325145167ab48df43cde9e5c8953d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332260"
---
# <a name="obtaining-bluetooth-address-of-hf-device"></a>HF デバイスの Bluetooth のアドレスの取得


HF デバイス トピックの取得の Bluetooth アドレスは、オーディオ ドライバーがハンズフリー (HF) のペアになっているデバイスの Bluetooth のアドレスを取得する方法について説明します。

アドレスの文字列は、特定のペアになっている HF デバイスを一意に識別するために役立ちます。 たとえば、アドレス文字列として使用できます、 *ReferenceString* IoRegisterDeviceInterface に渡されるパラメーター、 *RefString* KsCreateFilterFactory に渡されるパラメーター、または*名前*PcRegisterSubdevice に渡されるパラメーター。

なお、GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS デバイス インターフェイスのシンボリック リンクは一意も HF デバイスでは、各ペアになっていますが、何らの目的でこの文字列が長すぎますすることができます。

次のコード例に示すように、IoHelperGetDevicePdo ルーチンは、IoHelperGetDeviceBluetoothAddress で使用されるユーティリティ関数です。 オーディオ ドライバー、PnP インターフェイス着荷通知を処理している間、このような関数を呼び出すことができます。 オーディオ ドライバーでは、IoGetDeviceObjectPointer からデバイス オブジェクトを取得し、IoHelperGetDeviceBluetoothAddress に渡します。

```ManagedCPlusPlus
_IRQL_requires_(PASSIVE_LEVEL)
NTSTATUS
IoHelperGetDevicePdo(
    _In_ PDEVICE_OBJECT DeviceObject,
    _Out_ PDEVICE_OBJECT *PhysicalDeviceObject
    )

/*++

Routine description:
    Returns a pointer to the physical device object in a driver stack and
    increments the reference count on that object.

Parameters:
    DeviceObject
        Pointer to the device object for which the physical device object is
        retrieved. 

    PhysicalDeviceObject
        Returns a pointer to the physical device object in a stack of device
        objects after incrementing the reference count on the object.

Return value:
    A status code.

Remarks:
    This routine uses IRP_MN_QUERY_DEVICE_RELATIONS TargetDeviceRelation to
    get the physical device object from the device stack.

Requirements:
    IRQL    = PASSIVE_LEVEL

--*/

{
    NTSTATUS status;
    PIRP irp = NULL;
    PDEVICE_RELATIONS deviceRelations = NULL;
    PIO_STACK_LOCATION ioStack;
    KEVENT completionEvent;

    PAGED_CODE();

    irp = IoAllocateIrp(DeviceObject->StackSize, FALSE);
    if (irp == NULL)
    {
        status = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    irp->IoStatus.Status = STATUS_NOT_SUPPORTED;

    ioStack = IoGetNextIrpStackLocation(irp);
    ioStack->MajorFunction = IRP_MJ_PNP;
    ioStack->MinorFunction = IRP_MN_QUERY_DEVICE_RELATIONS;
    ioStack->Parameters.QueryDeviceRelations.Type = TargetDeviceRelation;

    KeInitializeEvent(&completionEvent, SynchronizationEvent, FALSE);

    IoSetCompletionRoutine(irp, OnRequestComplete, &completionEvent, TRUE, TRUE, TRUE);

    status = IoCallDriver(DeviceObject, irp);
    if (status == STATUS_PENDING) {
        // wait for irp to complete
        KeWaitForSingleObject(
            &completionEvent,
            Suspended,
            KernelMode,
            FALSE,
            NULL);
        status = irp->IoStatus.Status;
    }

    if (NT_SUCCESS(status))
    {
        deviceRelations = (PDEVICE_RELATIONS)irp->IoStatus.Information;
        *PhysicalDeviceObject = deviceRelations->Objects[0];
    }

Exit:
    if (deviceRelations != NULL)
    {
        ExFreePool(deviceRelations);
    }
    if (irp != NULL)
    {
        IoFreeIrp(irp);
    }
    return status;
}

_IRQL_requires_(PASSIVE_LEVEL)
NTSTATUS IoHelperGetDeviceBluetoothAddress(
    _In_ PDEVICE_OBJECT DeviceObject,
    _Outptr_ PWSTR *BluetoothAddress,
    _In_ ULONG Tag
    )

/*++

Routine description:
    Returns the Bluetooth address string for the physical device object in the
    device stack.

Parameters:
    DeviceObject
        Pointer to a device object in a device stack whose physical object has
        a Bluetooth address property.

    BluetoothAddress
        Returns a string allocated from NonPagedPoolNx pool. 

    Tag

Return value:
    A status code.

Remarks:
    This routine retrieves the DEVPKEY_Bluetooth_DeviceAddress property from
    the physical device object in the device stack containing the specified
    device object.

Requirements:
    IRQL    = PASSIVE_LEVEL

--*/

{
    NTSTATUS status;
    PDEVICE_OBJECT physicalDeviceObject = NULL;
    PWSTR bluetoothAddress = NULL;
    ULONG requiredSize;
    DEVPROPTYPE devPropType;

    PAGED_CODE();

    status = IoHelperGetDevicePdo(DeviceObject, &physicalDeviceObject);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    status = IoGetDevicePropertyData(physicalDeviceObject, &DEVPKEY_Bluetooth_DeviceAddress, LOCALE_NEUTRAL, 0, 0, NULL, &requiredSize, &devPropType);
    if (NT_SUCCESS(status) || devPropType != DEVPROP_TYPE_STRING)
    {
        status = STATUS_UNSUCCESSFUL;
        goto Exit;
    }
    if (status != STATUS_BUFFER_TOO_SMALL)
    {
        goto Exit;
    }

    bluetoothAddress = (PWCH)ExAllocatePoolWithTag(NonPagedPoolNx, requiredSize, Tag);
    if (bluetoothAddress == NULL)
    {
        status = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    status = IoGetDevicePropertyData(physicalDeviceObject, &DEVPKEY_Bluetooth_DeviceAddress, LOCALE_NEUTRAL, 0, requiredSize, bluetoothAddress, &requiredSize, &devPropType);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    *BluetoothAddress = bluetoothAddress;
    bluetoothAddress = NULL;
    status = STATUS_SUCCESS;

Exit:
    if (bluetoothAddress != NULL)
    {
        ExFreePoolWithTag(bluetoothAddress, Tag);
    }
    if (physicalDeviceObject != NULL)
    {
        ObDereferenceObject(physicalDeviceObject);
    }
    return status;
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[関連するデザインのガイドライン](related-design-guidelines.md)  




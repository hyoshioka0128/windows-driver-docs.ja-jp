---
title: デバイス レジスターの読み取りと書き込み
description: デバイス レジスターの読み取りと書き込み
ms.assetid: 58A94C75-94C1-4517-A300-9F04AA7B771A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c22fd5bdbc5547c6004a4d09fb5562b431afcaef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842212"
---
# <a name="reading-and-writing-to-device-registers"></a>デバイス レジスターの読み取りと書き込み


「[ハードウェアリソースの検索とマッピング](finding-and-mapping-hardware-resources.md)」で説明されているように、ドライバーがレジスタをマップした後、kmdf ドライバーは[**HAL ライブラリルーチン**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))を使用してレジスタに対する読み取りと書き込みを行いますが、通常、UMDF ドライバー (バージョン2.0 以降) は[WDF Register/を使用します。ポートアクセス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfhwaccess/)。

UMDF ドライバーがメモリマップトレジスタに直接アクセスする必要がある場合は、INF ディレクティブ**Umdfregisteraccessmode**を**RegisterAccessUsingUserModeMapping**に設定し、 [**WdfDeviceGetHardwareRegisterMappedAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegethardwareregistermappedaddress)を呼び出すことができます。ユーザーモードでマップされたアドレスを取得します。 フレームワークは、この方法で実行される読み取りおよび書き込みアクセスの検証を行わないため、レジスタアクセスにはこの手法を使用しないことをお勧めします。 UMDF INF ディレクティブの完全な一覧については、「 [WDF ディレクティブを INF ファイルで指定する](specifying-wdf-directives-in-inf-files.md)」を参照してください。

次の例には、KMDF (1.13 以降) または UMDF (2.0 以降) を使用してコンパイルできるコードが含まれています。 この例では、ドライバーが[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数を使用して、メモリマップトレジスタリソースを調べ、それらをユーザーモードアドレス空間にマップする方法を示しています。 この例では、メモリの場所にアクセスする方法を示します。

デバイスレジスタとポートにアクセスする前に、UMDF ドライバーは、ドライバーの INF ファイルで**UmdfDirectHardwareAccess**ディレクティブを**AllowDirectHardwareAccess**に設定する必要があります。

```cpp
NTSTATUS
 MyDevicePrepareHardware (
    IN WDFDEVICE  Device,
    IN WDFCMRESLIST  ResourcesRaw,
    IN WDFCMRESLIST  ResourcesTranslated
    )
  
{
    PCM_PARTIAL_RESOURCE_DESCRIPTOR desc = NULL;
    PCM_PARTIAL_RESOURCE_DESCRIPTOR  descTranslated = NULL;
    PHYSICAL_ADDRESS regBasePA = {0};
    ULONG regLength = 0;
    BOOLEAN found = FALSE;
    ULONG  i;
    PFDO_DATA deviceContext;
    NTSTATUS status = STATUS_SUCCESS;
    
    UNREFERENCED_PARAMETER(ResourcesRaw);

    MyKdPrint(("MyEvtDevicePrepareHardware Device 0x%p ResRaw 0x%p ResTrans "
        "0x%p Count %d\n", Device, ResourcesRaw, ResourcesTranslated,
        WdfCmResourceListGetCount(ResourcesTranslated)));

#ifndef _KERNEL_MODE
    WDF_DEVICE_IO_TYPE stackReadWriteIotype = WdfDeviceIoUndefined; 
    WDF_DEVICE_IO_TYPE stackIoctlIotype = WdfDeviceIoUndefined;
    WdfDeviceGetDeviceStackIoType(Device,
                                  &stackReadWriteIotype,
                                  &stackIoctlIotype);
    MyKdPrint(("Device 0x%p stackReadWriteIoType %S stackIoctlIoType %S\n",
        Device,
        GetIoTypeName(stackReadWriteIotype),
        GetIoTypeName(stackIoctlIotype)
        ));

#endif

    deviceContext = ToasterFdoGetData(Device);
    
    //
    // Scan the list and identify our resource
    //
    for (i = 0; i < WdfCmResourceListGetCount(ResourcesTranslated); i++) {
        desc = WdfCmResourceListGetDescriptor(Resources, i);
        descTranslated =  WdfCmResourceListGetDescriptor(ResourcesTranslated, i);
           
        switch (desc->Type) {
            case CmResourceTypeMemory:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypeMemory resources \n"));
                //
                // see if this is the memory resource we're looking for
                // 
                if (desc->u.Memory.Length == 0x200) {
                    regBasePA = desc->u.Memory.Start;
                    regLength = desc->u.Memory.Length;
                    found = TRUE;                    
                }
                break;
                
            case CmResourceTypePort:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypePort"
                    " resource\n"));

                switch(descTranslated->Type) {

                case CmResourceTypePort:
                    deviceContext->PortWasMapped = FALSE;
                    deviceContext->PortBase = 
                        ULongToPtr(descTranslated->u.Port.Start.LowPart);
                    deviceContext->PortCount = descTranslated ->u.Port.Length;
                    MyKdPrint(("Resource Translated Port: (%x) Length: (%d)\n",
                             descTranslated->u.Port.Start.LowPart,
                             descTranslated->u.Port.Length));                        
                    break;
                    
                case CmResourceTypeMemory:
                    //
                    // Map the memory
                    //

#if IS_UMDF_DRIVER                    
                    status = WdfDeviceMapIoSpace(
                                            Device,
                                            descTranslated->u.Memory.Start,
                                            descTranslated->u.Memory.Length,
                                            MmNonCached,
                                            &deviceContext->PortBase
                                            );

                    if (!NT_SUCCESS(status)) {
                        WdfVerifierDbgBreakPoint();
                    }
#else
                    deviceContext->PortBase = (PVOID) 
                                        MmMapIoSpace(
                                            descTranslated->u.Memory.Start,
                                            descTranslated->u.Memory.Length,
                                            MmNonCached
                                            );
                    UNREFERENCED_PARAMETER(status);

#endif
                    deviceContext->PortCount = descTranslated->u.Memory.Length;
                    deviceContext->PortWasMapped = TRUE;
                    MyKdPrint(("Resource Translated Memory: (%x) Length: (%d)\n",
                             descTranslated->u.Memory.Start.LowPart,
                             descTranslated->u.Memory.Length));                        
                    break;
                default:
                    MyKdPrint(("Unhandled resource_type (0x%x)\n", 
                        descTranslated->Type));
                }
                break;

            case CmResourceTypeInterrupt:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypeInterrupt"
                    "resource\n"));
                break;                

            case CmResourceTypeConnection:
                MyKdPrint(("EvtPrepareHardware: found CmResourceTypeConnection"
                    "resource\n"));
                break;                

            default:
                MyKdPrint(("EvtPrepareHardware: found resources of type %d"
                    "(CM_RESOURCE_TYPE)\n", desc->Type));
                break;
        }
    }


//
// Next, the driver uses register/port access macros to access the port.
//

    if ((PUCHAR)&deviceContext->PortBase != NULL) {
        UCHAR data;
        
#ifndef _KERNEL_MODE
        data = WDF_READ_PORT_UCHAR(Device, (PUCHAR)deviceContext->PortBase);
#else
        data = READ_PORT_UCHAR((PUCHAR)deviceContext->PortBase);
#endif

        MyKdPrint(("Read value %d from port address 0x%p\n", data, 
            deviceContext->PortBase));
    }
  
  if (i == 0) {
        MyKdPrint(("EvtPrepareHardware: no cm resources found \n"));
    }
    
    return STATUS_SUCCESS;
}



NTSTATUS
 MyDeviceReleaseHardware (
    IN WDFDEVICE  Device,
    IN WDFCMRESLIST  ResourcesTranslated
    )

{
    PFDO_DATA deviceContext;

    UNREFERENCED_PARAMETER(ResourcesTranslated);

    MyKdPrint(("CovEvtDeviceReleaseHardware Device 0x%p ResTrans 0x%p\n", 
        Device, ResourcesTranslated));

    deviceContext = ToasterFdoGetData(Device);

    if (deviceContext->PortWasMapped) {
#if IS_UMDF_DRIVER
        WdfDeviceUnmapIoSpace(Device,
                              deviceContext->PortBase,
                              deviceContext->PortCount);
#else
        MmUnmapIoSpace(deviceContext->PortBase,
                     deviceContext->PortCount);
#endif
    }

    return STATUS_SUCCESS;
}
```

 

 






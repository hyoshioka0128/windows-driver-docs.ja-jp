---
title: デバイス レジスターの読み取りと書き込み
description: デバイス レジスターの読み取りと書き込み
ms.assetid: 58A94C75-94C1-4517-A300-9F04AA7B771A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6584ea910624f07992ab6c3d40e1a86cfb973f6
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349833"
---
# <a name="reading-and-writing-to-device-registers"></a>デバイス レジスターの読み取りと書き込み


」の説明に従って、ドライバーのレジスタがマップする後[マッピング ハードウェア リソースの検索と](finding-and-mapping-hardware-resources.md)、KMDF ドライバーを使用して、 [ **HAL ライブラリ ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff546644)読み取りし、書き込みをする登録すると、通常 UMDF ドライバー (バージョン 2.0 以降) を使用中に、 [WDF 登録/ポート アクセス関数](https://msdn.microsoft.com/library/windows/hardware/dn265662)します。

INF ディレクティブを設定できる UMDF ドライバーでは、メモリ マップト レジスタに直接アクセスする必要があるを場合**UmdfRegisterAccessMode**に**RegisterAccessUsingUserModeMapping**を呼び出して[ **WdfDeviceGetHardwareRegisterMappedAddress** ](https://msdn.microsoft.com/library/windows/hardware/dn265603)ユーザー モードを取得するアドレスをマップします。 フレームワークは、読み取りを検証し、この方法で実行するアクセスの書き込みありません、ため、この手法はレジスタへのアクセスは推奨されません。 UMDF INF ディレクティブの一覧については、[INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)を参照してください。

次の例には、KMDF (1.13 またはそれ以降) または UMDF (2.0 以降) を使用してコンパイルでしたコードが含まれています。 ドライバーの使用方法の例を示します、 [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)そのメモリ マップト登録リソースを確認し、ユーザー モード アドレス空間にマップするコールバック関数。 例は、メモリの場所にアクセスする方法を示します。

デバイスの登録とポートへのアクセスをする前に、UMDF ドライバーを設定する必要があります、 **UmdfDirectHardwareAccess**ディレクティブを**AllowDirectHardwareAccess**ドライバーの INF ファイルでします。

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

 

 






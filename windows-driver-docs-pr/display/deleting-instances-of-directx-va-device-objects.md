---
title: DirectX VA デバイス オブジェクトのインスタンスの削除
description: DirectX VA デバイス オブジェクトのインスタンスの削除
ms.assetid: fab8c6eb-97fa-427e-9fb2-6da249d8d97d
keywords:
- DirectX VA デバイス オブジェクトのインスタンスを削除します。
- DirectX VA デバイス オブジェクトのインスタンスの削除
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、インスタンスの削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 140414cebfb2a6d3ef7fda237e9844e26907b780
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384895"
---
# <a name="deleting-instances-of-directx-va-device-objects"></a>DirectX VA デバイス オブジェクトのインスタンスの削除


## <span id="ddk_deleting_instances_of_directx_va_device_objects_gg"></span><span id="DDK_DELETING_INSTANCES_OF_DIRECTX_VA_DEVICE_OBJECTS_GG"></span>


DirectX VA デバイス オブジェクトのインスタンスを削除するのにには、次のコード例を使用します。 このコードは、の実装、 [ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)コールバック関数。 **DestroyMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)コールバック関数へのポインターを構造体します。

```cpp
DWORD APIENTRY
  MOCOMPCB_DESTROY(
    PDD_DESTROYMOCOMPDATA  lpData
    )
{
    // The driver saves the device class object in lpDriverReserved1 
     // during the call to the DdMoCompCreate callback. For more information, 
     // see Creating Instances of DirectX VA Device Objects.
 DXVA_DeviceBaseClass* pDXVABase =
          (DXVA_DeviceBaseClass*)lpData->lpMoComp->lpDriverReserved1;
 if (pDXVABase == NULL) {
        lpData->ddRVal = E_POINTER;
        return DDHAL_DRIVER_HANDLED;
    }
    // Process according to the device type in the class object.
     // For more information, see Defining DirectX VA Device Classes.
    switch (pDXVABase->m_DeviceType) {
    // This is the deinterlace container device.
    case DXVA_DeviceContainer:
        lpData->ddRVal = S_OK;
        delete pDXVABase;
        break;

    // This is the ProcAmp control device.
 case DXVA_DeviceProcAmpControl:
        {
            DXVA_ProcAmpControlDeviceClass* pDXVADev =
 (DXVA_ProcAmpControlDeviceClass*)pDXVABase;
             // Part of the ProcAmp Control DDI.
            lpData->ddRVal = pDXVADev->ProcAmpControlCloseStream();
            delete pDXVADev;
        }
        break;

    // This is the deinterlace bob device.
 case DXVA_DeviceDeinterlacer:
        {
            DXVA_DeinterlaceBobDeviceClass* pDXVADev =
 (DXVA_DeinterlaceBobDeviceClass*)pDXVABase;
             // Part of the Deinterlace DDI.
            lpData->ddRVal = pDXVADev->DeinterlaceCloseStream();
            delete pDXVADev;
        }
        break;

    // This is the COPP device.
    case DXVA_DeviceCOPP:
        DXVA_COPPDeviceClass* pDXVADev = (DXVA_COPPDeviceClass*)pDXVABase;
        ULONG BytesReturned;
        HANDLE handle = (HANDLE)GetDriverHandleFromPDEV(lpData ->lpDD->lpGbl->dhpdev)
        COPP_IO_InputBuffer InputBuffer;
        InputBuffer.ppThis = &pDXVADev->m_pThis;
        InputBuffer.InputBuffer = NULL;
        InputBuffer.phr = &lpData->ddRVal;
        EngDeviceIoControl(handle,
                           IOCTL_COPP_CloseDevice,
                           &InputBuffer,
                           sizeof(InputBuffer),
                           NULL,
                           0,
                           &BytesReturned);
            delete pDXVADev;
        }
        break;
    }
    return DDHAL_DRIVER_HANDLED;
}
```

 

 






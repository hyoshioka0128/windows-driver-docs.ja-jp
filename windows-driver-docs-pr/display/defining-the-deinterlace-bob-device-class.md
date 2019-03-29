---
title: デインターレース bob デバイス クラスの定義
description: デインターレース bob デバイス クラスの定義
ms.assetid: 1efe0a08-c3aa-4083-a19f-96e5ba94d517
keywords:
- WDK の DirectX va なので、bob デインター レース
- WDK DirectX VA デインター レースを bob します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7845cb8019d32368980e189bab971a3a3801ef9
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349873"
---
# <a name="defining-the-deinterlace-bob-device-class"></a>デインターレース bob デバイス クラスの定義


## <span id="ddk_defining_the_deinterlace_bob_device_class_gg"></span><span id="DDK_DEFINING_THE_DEINTERLACE_BOB_DEVICE_CLASS_GG"></span>


インター bob のデバイス クラスを定義するのにには、次のコード例を使用します。

```cpp
// Deinterlace bob device class.
struct DXVA_DeinterlaceBobDeviceClass : public DXVA_DeviceBaseClass
{
    DXVA_VideoDesc  m_VideoDesc;
    // Uses the base class's constructor.
    DXVA_DeinterlaceBobDeviceClass(const GUID& guid, DXVA_DeviceType Type) :
        DXVA_DeviceBaseClass(guid, Type)
    {}
    // The following functions are part of the 
     // Deinterlace DDI.
    HRESULT DeinterlaceOpenStream(LPDXVA_VideoDesc lpVideoDescription);
    HRESULT DeinterlaceCloseStream();
    HRESULT DeinterlaceBlt(
                           REFERENCE_TIME  rtTargetFrame,
                           LPRECT  lprcDstRect,
                           LPDDSURFACE  lpDDSDstSurface,
                           LPRECT  lprcSrcRect,
                           LPDXVA_VideoSample  lpDDSrcSurfaces,
                           DWORD  dwNumSurfaces,
                           FLOAT  fAlpha);
    HRESULT DeinterlaceBltEx(
                           REFERENCE_TIME  rtTargetFrame,
                           LPRECT  lprcTargetRect,
                           DXVA_AYUVsample2  BackgroundColor,
                           DWORD  dwDestinationFormat,
                           DWORD  dwDestinationFlags,
                           LPDDSURFACE  lpDDSDstSurface,
                           LPDXVA_VideoSample2  lpDDSrcSurfaces,
                           DWORD  dwNumSurfaces,
                           FLOAT  fAlpha);
};
```

 

 






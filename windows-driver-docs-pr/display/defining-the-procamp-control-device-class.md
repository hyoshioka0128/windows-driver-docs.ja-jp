---
title: ProcAmp コントロール デバイス クラスを定義します。
description: ProcAmp コントロール デバイス クラスを定義します。
ms.assetid: 382f5ecf-ce87-4100-adc7-7006cc7dc5ed
keywords:
- ProcAmp WDK DirectX va なので、デバイス クラスを定義します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91d9a51f0746970355d8a35362f1f9e48bb91ad1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551278"
---
# <a name="defining-the-procamp-control-device-class"></a>ProcAmp コントロール デバイス クラスを定義します。


## <span id="ddk_defining_the_procamp_control_device_class_gg"></span><span id="DDK_DEFINING_THE_PROCAMP_CONTROL_DEVICE_CLASS_GG"></span>


ProcAmp コントロール デバイス クラスを定義するのにには、次のコード例を使用します。

```cpp
// ProcAmp control device class.
struct DXVA_ProcAmpControlDeviceClass : public DXVA_DeviceBaseClass
{
    DXVA_VideoDesc  m_VideoDesc;
    // Uses the base class&#39;s constructor.
    DXVA_ProcAmpControlDeviceClass(const GUID& guid, DXVA_DeviceType Type) :
        DXVA_DeviceBaseClass(guid, Type)
    {}
    // The following three functions are part of the 
     // ProcAmp Control DDI.
    HRESULT ProcAmpControlOpenStream(LPDXVA_VideoDesc lpVideoDescription);
    HRESULT ProcAmpControlCloseStream();
    HRESULT ProcAmpControlBlt(
                           LPVOID lpDDSDstSurface,
                           LPVOID lpDDSSrcSurface,
                           DXVA_ProcAmpControlBlt* pCcBlt);
};
```

 

 






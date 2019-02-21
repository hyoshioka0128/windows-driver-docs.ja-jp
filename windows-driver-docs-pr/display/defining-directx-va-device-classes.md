---
title: DirectX VA デバイス クラスを定義します。
description: DirectX VA デバイス クラスを定義します。
ms.assetid: a4b2ee88-747a-48c3-ba1d-2d605c46db58
keywords:
- デバイス クラスを定義する、DirectX ビデオ アクセラレータ WDK Windows 2000 の表示
- デバイスは、WDK DirectX VA をクラスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a95ad517c67d0ec418cfafc4d99749eca8e0ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539230"
---
# <a name="defining-directx-va-device-classes"></a>DirectX VA デバイス クラスを定義します。


## <span id="ddk_defining_directx_va_device_classes_gg"></span><span id="DDK_DEFINING_DIRECTX_VA_DEVICE_CLASSES_GG"></span>


このセクションではインター コンテナー デバイス、ProcAmp 制御デバイス、インター モードのデバイスのデバイス クラスを定義するコード例を使用して (たとえば、 [bob](bob-deinterlacing.md)) と COPP デバイス。 これらのデバイス クラスを構成するメンバー関数の宣言を含めることが、 [ProcAmp コントロール DDI](https://msdn.microsoft.com/library/windows/hardware/ff569186)と[インター レースを解除 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552701)します。 これらのデバイス クラス定義は、ドライバーによって提供されるヘッダー ファイルで宣言できます。

各デバイスの種類と各デバイスの種類に適用される基本クラスを定義するのにには、次のコード例を使用します。

```cpp
// These enumerated types specify the DirectX VA device class.
enum DXVA_DeviceType {
    DXVA_DeviceContainer        = 0x0001,
    DXVA_DeviceDecoder          = 0x0002,
    DXVA_DeviceDeinterlacer     = 0x0003,
     DXVA_DeviceProcAmpControl   = 0x0004,
    DXVA_DeviceCOPP             = 0x0005
};
// Other DirectX VA device classes inherit from this base class, 
struct DXVA_DeviceBaseClass {
    GUID            m_DeviceGUID;
    DXVA_DeviceType m_DeviceType;

    DXVA_DeviceBaseClass(const GUID& guid, DXVA_DeviceType Type) :
        m_DeviceGUID(guid), m_DeviceType(Type)
    {}
};
```

次のトピックには、インター コンテナー デバイス、ProcAmp 制御デバイス、インター bob デバイス、および COPP デバイスのクラスを定義するコード例が含まれます。

[定義する、コンテナーのデバイス クラスのインター レースを解除](defining-the-deinterlace-container-device-class.md)

[ProcAmp コントロール デバイス クラスを定義します。](defining-the-procamp-control-device-class.md)

[インター Bob デバイス クラスを定義します。](defining-the-deinterlace-bob-device-class.md)

[COPP デバイス クラスを定義します。](defining-the-copp-device-class.md)

 

 






---
title: コールバック オブジェクトの例を作成します。
description: コールバック オブジェクトの例を作成します。
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- コールバック オブジェクト WDK UMDF、作成する例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19f852def4de16f87cef0b970f1ed39e78ca9024
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560753"
---
# <a name="creating-callback-objects-example"></a>コールバック オブジェクトの例を作成します。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次のコード例は、の実装では、ドライバーがデバイス コールバック オブジェクトを作成する方法を示していますその[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)メソッドと、デバイス コールバックへのポインターを渡します。インターフェイスの呼び出しで、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)デバイスを作成するメソッド。

```cpp
   HRESULT CMyDriver::OnDeviceAdd(
              IWDFDriver*           pDriver,
              IWDFDeviceInitialize* pDeviceInit
              ) {
      IUnknown *pDeviceCallback = NULL;
      ...
      HRESULT hr;
      // Create callback object
      hr = CMyDevice::CreateInstance( &pDeviceCallback,
                                      pDeviceInit,
                                      completionPort );
      ...
      // Create WDF device
      hr = pDriver->CreateDevice( pDeviceInit, 
                                  pDeviceCallback,
                                  &pIWDFDevice );
      ...
   }
```

 

 






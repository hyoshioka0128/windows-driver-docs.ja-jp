---
title: コールバック オブジェクトの作成の例
description: コールバック オブジェクトの作成の例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- コールバック オブジェクト WDK UMDF、作成する例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca08be818e342e761830418ff1183e64a1fd6f56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382394"
---
# <a name="creating-callback-objects-example"></a>コールバック オブジェクトの作成の例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次のコード例は、の実装では、ドライバーがデバイス コールバック オブジェクトを作成する方法を示していますその[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドと、デバイス コールバックへのポインターを渡します。インターフェイスの呼び出しで、 [ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)デバイスを作成するメソッド。

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

 

 






---
title: コールバック オブジェクトの作成の例
description: コールバック オブジェクトの作成の例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- コールバックオブジェクト WDK UMDF、作成の例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 826efa4bca1593569ac46755fb74a0b06178727f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210222"
---
# <a name="creating-callback-objects-example"></a>コールバック オブジェクトの作成の例


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

次のコード例は、ドライバーが[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドの実装にデバイスコールバックオブジェクトを作成し、 [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドへの呼び出しにデバイスコールバックインターフェイスへのポインターを渡してデバイスを作成する方法を示しています。

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

 

 






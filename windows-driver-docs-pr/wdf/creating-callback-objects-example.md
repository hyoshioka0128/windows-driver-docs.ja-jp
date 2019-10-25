---
title: コールバック オブジェクトの作成の例
description: コールバック オブジェクトの作成の例
ms.assetid: 4476c2f0-12ba-4678-b20e-bde7e81df01d
keywords:
- コールバックオブジェクト WDK UMDF、作成の例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327c02d71a27bbe41851883dfced880ca614470e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845604"
---
# <a name="creating-callback-objects-example"></a>コールバック オブジェクトの作成の例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次のコード例では、ドライバーが[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドの実装にデバイスコールバックオブジェクトを作成し、 [**Iwdfdriver:: CreateDevice への呼び出しでデバイスコールバックインターフェイスへのポインターを渡す方法を示しています。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)デバイスを作成するメソッド。

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

 

 






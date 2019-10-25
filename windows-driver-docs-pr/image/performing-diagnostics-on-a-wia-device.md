---
title: WIA デバイスでの診断の実行
description: WIA デバイスでの診断の実行
ms.assetid: 15962c49-f03c-409b-b138-033893a50ec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02d76c9958b5cd89299d9f8bda6722737bc1b436
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840775"
---
# <a name="performing-diagnostics-on-a-wia-device"></a>WIA デバイスでの診断の実行





WIA サービスでは、 [**Istiusd::D iとらわれ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic)ないメソッドを呼び出すことによって、デバイスの機能状態をテストできます。 WIA ミニドライバーは、ハードウェアの現在の機能状態を確認し、結果を報告する必要があります。 **I:D i無関係**のメソッドは、WIA デバイスの既定のプロパティページ (Microsoft が提供するプロパティページ) で [テストデバイス] ボタンが押されたときにも呼び出されます。

次の例では、 **ib usd::D iとらわれ**ないメソッドの実装を示します。

```cpp
STDMETHODIMP CWIADevice::Diagnostic(LPSTI_DIAG pBuffer)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if(!pBuffer){
     return E_INVALIDARG;
  }

  //
  // initialize response buffer
  //

  memset(&pBuffer->sErrorInfo,0,sizeof(pBuffer->sErrorInfo));

  pBuffer->sErrorInfo.dwGenericError = NOERROR;
  pBuffer->sErrorInfo.dwVendorError  = 0;

  HRESULT hr = S_OK;
  if(!TestMyDeviceFunctionalty()) {
    pBuffer->sErrorInfo.dwGenericError = E_FAIL; // win32 generic error code
    pBuffer->sErrorInfo.dwVendorError  = 1234;   // device specific vendor error code
  }
  return hr;
}
```

 

 





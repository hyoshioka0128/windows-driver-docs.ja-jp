---
title: WIA デバイスでの診断の実行
description: WIA デバイスでの診断の実行
ms.assetid: 15962c49-f03c-409b-b138-033893a50ec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ff78cc4d2a51078109eee2589dbdcb94ed44d60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327851"
---
# <a name="performing-diagnostics-on-a-wia-device"></a>WIA デバイスでの診断の実行





WIA サービスは呼び出すことによって機能のデバイスの状態をテストすることができます、 [ **IStiUSD::Diagnostic** ](https://msdn.microsoft.com/library/windows/hardware/ff543814)メソッド。 WIA ミニドライバーをハードウェアの現在の機能の状態を確認し、結果を報告します。 **IStiUSD::Diagnostic** WIA デバイスの既定のプロパティ ページ (Microsoft 提供のプロパティ ページ) で、「テスト デバイス」ボタンが押されたときに、メソッドが呼び出されます。

次の例の実装を示しています、 **IStiUSD::Diagnostic**メソッド。

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

 

 





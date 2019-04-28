---
title: 切断された可能性のあるデバイスの通信の確立を試みるためのコード例
description: 切断された可能性のあるデバイスの通信の確立を試みるためのコード例
ms.assetid: 74633481-229f-4074-a84e-cc515eaaacd0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31638e6a26d664fb817ddd76228d915811329eb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373215"
---
# <a name="code-example-for-challenging-a-potentially-disconnected-device"></a>切断された可能性のあるデバイスの通信の確立を試みるためのコード例

> [!IMPORTANT]  
> WSD 見据えて機能は非推奨とされているし、WSD の挑戦者に関連するすべてのドキュメントは、2018 年に削除されます。

次のコード例への呼び出しを示しています、 **RegisterDeviceToChallenge**関数 (コード例にリストされている[ヘルパー メソッドを実装するためのサンプル コード](code-example-for-implementing-helper-methods.md)) チャレンジに、可能性がありますデバイスを切断します。

```cpp
HRESULT hr = S_OK;

if (SUCCEEDED(hr))
{
    //
    // Activate ScanProxy to retrieve the IScanService interface for it
    //
    hr = m_pFunctionInstance->QueryService(__uuidof(WSDScanProxy),
                                           __uuidof(IScanService),
                                           (void**) &m_pScanProxy);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "IFunctionInstance::QueryService(WSDScanProxy, IScanService) failed, cannot activate ScanProxy, hr = 0x%08X", hr));
 
        if (WSD_COMMUNICATION_ERROR(hr))
        {
            RegisterDeviceToChallenge();
        }
    }
}

if (SUCCEEDED(hr))
{
    //
    // Retrieve the IScanServiceEvents interface from the ScanProxy
    //
    hr = m_pScanProxy->QueryInterface(__uuidof(IScanServiceEvents), (void**)&m_pScanEvents);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "IScanService::QueryInterface(IScanServiceEvents) failed, hr = 0x%08X", hr));
 
        if (WSD_COMMUNICATION_ERROR(hr))
        {
            RegisterDeviceToChallenge();
        }
    }
}
```

 

 





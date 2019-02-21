---
title: デバイスのプロパティを初期化するためのコード例
description: デバイスのプロパティを初期化するためのコード例
ms.assetid: ec25fa77-13d8-4cb0-913c-b24010355702
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99f59aba3a32ce7b3b080331c7a64941a41dc9a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538339"
---
# <a name="code-example-for-initializing-device-properties"></a>デバイスのプロパティを初期化するためのコード例


中に、 [ **IWiaMiniDrv::drvInitItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff544989)ルート アイテム、ミニドライバーの呼び出しは、デバイスを記述する次の WIA プロパティを初期化する必要があります。

[**WIA\_DPS\_サービス\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551428)

[**WIA\_DPS\_デバイス\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551374)

[**WIA\_DPS\_GLOBAL\_の ID**](https://msdn.microsoft.com/library/windows/hardware/ff551395)

[**WIA\_DPA\_ファームウェア\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff550309)

次のコード例は、WIA を初期化する方法を示します\_DPS\_サービス\_ID を使用して、 **OpenProperyStore**と**ReadDeviceProperty**を読み取るメソッド鍵\_PNPX\_ServiceId します。 同じ一般的な方法は、各デバイスのプロパティを初期化するために使用できます。

```cpp
HRESULT hr = S_OK;
IPropertyStore *pPropertyStore = NULL;
BSTR bstrPropertyValue = NULL;

//
// Open the current Property Store and keep it opened until all needed properties are read
//
if (SUCCEEDED(hr))
{
    hr = OpenPropertyStore(&pPropertyStore);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "Failed to open the Property Store for the current Function Instance, hr = 0x%08X", hr));
    }
}

//
// Initialize WIA_DPS_SERVICE_ID
//
if (SUCCEEDED(hr))
{
    hr = ReadDeviceProperty(pPropertyStore, &PKEY_PNPX_ServiceId, &bstrPropertyValue);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "Failed to read the PKEY_PNPX_ServiceId device property, hr = 0x%08X", hr));
    }

    if ((SUCCEEDED(hr)) && (bstrPropertyValue)) 
    {
        WIAS_TRACE((g_hInst, "Service id: %ws", (LPWSTR)bstrPropertyValue));
 
        hr = AddProperty(WIA_DPS_SERVICE_ID, WIA_DPS_SERVICE_ID_STR, RN, bstrPropertyValue);
        if (FAILED(hr)) 
        {
            WIAS_ERROR((g_hInst, "Failed to add WIA_DPS_SERVICE_ID property to the property manager, hr = 0x%08X", hr));
        }
    }

    if (bstrPropertyValue)
    {
        SysFreeString(bstrPropertyValue);
        bstrPropertyValue = NULL;
    }
}

//
// Repeat the same procedure for WIA_DPS_DEVICE_ID, WIA_DPS_GLOBAL_IDENTITY, and WIA_DPS_FIRMWARE_VERSION
//

//
// Close the Property Store
//
if (pPropertyStore)
{
    pPropertyStore->Release();
    pPropertyStore = NULL;
}
```

 

 





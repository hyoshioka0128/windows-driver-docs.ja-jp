---
title: デバイス プロパティを初期化するためのコード例
description: デバイス プロパティを初期化するためのコード例
ms.assetid: ec25fa77-13d8-4cb0-913c-b24010355702
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0b69445392be4fcd71f456ab155373dd720460a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840872"
---
# <a name="code-example-for-initializing-device-properties"></a>デバイス プロパティを初期化するためのコード例


ルート項目の[**IWiaMiniDrv::D rvinititemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)呼び出し中に、ミニドライバーは、デバイスを記述する次の WIA プロパティを初期化する必要があります。

[**WIA\_DPS\_サービス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-service-id)

[**WIA\_DPS\_デバイス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-device-id)

[**WIA\_DPS\_グローバル\_ID**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-global-identity)

[**WIA\_DPA\_ファームウェア\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dpa-firmware-version)

次のコード例では、OpenPKEY\_PNPX\_ServiceId を読み取るために**open**および**readdeviceproperty**メソッドを使用して、WIA\_DPS\_サービス\_ID を初期化する方法を示します。 同じ一般的な方法を使用して、各デバイスプロパティを初期化できます。

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

 

 





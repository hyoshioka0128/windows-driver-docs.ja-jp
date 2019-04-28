---
Description: サポートされているファイル形式プロパティの取得
title: サポートされているファイル形式プロパティの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13b9f56445c052333adcf74069fcd12412d8cfdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376190"
---
# <a name="supported-format-property-retrieval"></a>サポートされているファイル形式プロパティの取得


WPD アプリケーションを呼び出すと、 **IPortableDeviceCapabilities::GetSupportedFormatProperties**メソッドでは、このメソッドは、さらへの呼び出しをトリガー、 **WpdCapabilities::OnGetSupportedFormatProperties**サンプル ドライバーでのメソッド。 後者のメソッドを作成、 **IPortableDeviceKeyCollection**先、ドライバーがサポート、特定形式のオブジェクトのプロパティを格納するオブジェクト。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetSupportedFormatProperties(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr               = S_OK;
    GUID    guidObjectFormat = GUID_NULL;
    CComPtr<IPortableDeviceKeyCollection> pKeys;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the object format whose supported properties have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FORMAT, &guidObjectFormat);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_FORMAT");
    }

    // CoCreate a collection to store the supported properties.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceKeyCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceKeyCollection,
                              (VOID**) &pKeys);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceKeyCollection");
    }

    // Add the supported properties for the specified object format to the collection.
    if (hr == S_OK)
    {
        hr = AddSupportedPropertyKeys(guidObjectFormat, pKeys);
        CHECK_HR(hr, "Failed to get supported properties for a format");
    }

    // Set the WPD_PROPERTY_CAPABILITIES_PROPERTY_KEYS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIPortableDeviceKeyCollectionValue(WPD_PROPERTY_CAPABILITIES_PROPERTY_KEYS, pKeys);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_PROPERTY_KEYS");
    }

    return hr;
}
```

 

 





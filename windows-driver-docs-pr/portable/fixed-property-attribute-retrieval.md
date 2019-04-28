---
Description: 固定プロパティ属性の取得
title: 固定プロパティ属性の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61f8a57acb7d91fe37daa32b9fe93bf0560f7d0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378168"
---
# <a name="fixed-property-attribute-retrieval"></a>固定プロパティ属性の取得


WPD アプリケーションを呼び出すと、 **IPortableDeviceCapabilities::GetFixedPropertyAttributes**メソッドでは、このメソッドは、さらへの呼び出しをトリガー、 **WpdCapabilities::OnGetFixedPropertyAttributes**サンプル ドライバーでのメソッド。 後者のメソッドを作成、 **IPortableDeviceValues**にドライバーが要求された属性を格納するオブジェクト。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetFixedPropertyAttributes(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT     hr               = S_OK;
    GUID        guidObjectFormat = GUID_NULL;
    PROPERTYKEY key              = WPD_PROPERTY_NULL;
    CComPtr<IPortableDeviceValues> pAttributes;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the object format whose fixed property attributes have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FORMAT, &guidObjectFormat);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_FORMAT");
    }

    // Get the property whose fixed property attributes have been requested
    if(hr == S_OK)
    {
        hr = pParams->GetKeyValue(WPD_PROPERTY_CAPABILITIES_PROPERTY_KEYS, &key);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_PROPERTY_KEYS");
    }

    // CoCreate a collection to store the fixed property attributes.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pAttributes);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValues");
    }

    // Add the fixed property attributes for the specified object format and property
    if (hr == S_OK)
    {
        hr = GetFixedPropertyAttributesForFormat(guidObjectFormat, key, pAttributes);
        CHECK_HR(hr, "Failed to get fixed property attributes");
    }

    // Set the WPD_PROPERTY_CAPABILITIES_PROPERTY_ATTRIBUTES value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIPortableDeviceValuesValue(WPD_PROPERTY_CAPABILITIES_PROPERTY_ATTRIBUTES, pAttributes);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_PROPERTY_ATTRIBUTES");
    }

    return hr;
}
```

 

 





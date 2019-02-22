---
Description: Supported Format Retrieval
title: サポートされている形式の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe13842d484d0731683bd66972bcbdb7f8194ef7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535473"
---
# <a name="supported-format-retrieval"></a>サポートされている形式の取得


WPD アプリケーションを呼び出すと、 **IPortableDeviceCapabilities::GetSupportedFormats**メソッドでは、このメソッドは、さらへの呼び出しをトリガー、 **WpdCapabilities::OnGetSupportedFormats**メソッドで、ドライバーのサンプルです。 後者のメソッドを作成、 **IPortableDevicePropVariantCollection**にドライバーが特定のコンテンツ タイプでサポートされる形式を格納するオブジェクト。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetSupportedFormats(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr              = S_OK;
    GUID    guidContentType = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pFormats;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the content type whose supported formats have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_CONTENT_TYPE, &guidContentType);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_CONTENT_TYPE");
    }

    // CoCreate a collection to store the supported formats.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pFormats);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported formats for the specified content type to the collection.
    if (hr == S_OK)
    {
        PROPVARIANT pv = {0};
        PropVariantInit(&pv);
        // Don&#39;t call PropVariantClear, since we did not allocate the memory for these GUIDs

        if ((guidContentType   == WPD_CONTENT_TYPE_DOCUMENT) ||
            ((guidContentType  == WPD_CONTENT_TYPE_ALL)))
        {
            // Add WPD_OBJECT_FORMAT_TEXT to the supported formats collection
            pv.vt    = VT_CLSID;
            pv.puuid = (CLSID*)&WPD_OBJECT_FORMAT_TEXT;
            hr = pFormats->Add(&pv);
            CHECK_HR(hr, "Failed to add WPD_OBJECT_FORMAT_TEXT");
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_FORMATS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_FORMATS, pFormats);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_FORMATS");
    }

    return hr;
}
```

 

 





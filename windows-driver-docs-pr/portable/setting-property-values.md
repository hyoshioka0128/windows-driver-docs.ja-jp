---
Description: プロパティ値の設定
title: プロパティ値の設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 214d50bc3d70a8ffd27ff5f48d93477fe583a426
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376216"
---
# <a name="setting-property-values"></a>プロパティ値の設定


WPD アプリケーションを呼び出すと、 **IPortableDeviceProperties::SetValues**メソッドでは、このメソッドは、さらへの呼び出しをトリガー、 **WpdObjectProperties::OnSetPropertyValues**サンプル ドライバー メソッド. このメソッドを作成、 **IPortableDeviceValues**オブジェクトに新しい値が書き込まれます。 ただし、ドライバーのサンプルでは、そのプロパティのいずれかで更新することはできません、ため、このメソッドは書き込みます E\_内の各エントリを対象として ACCESSDENIED、 **IPortableDeviceValues**オブジェクト。

```ManagedCPlusPlus
HRESULT WpdObjectProperties::OnSetPropertyValues(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr          = S_OK;
    LPWSTR  wszObjectID = NULL;
    DWORD   cValues     = 0;
    CComPtr<IPortableDeviceValues> pValues;
    CComPtr<IPortableDeviceValues> pWriteResults;
    CComPtr<IPortableDeviceValues> pEventParams;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the object identifier whose property values are being set
    if (hr == S_OK)
    {
        hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID, &wszObjectID);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID");
    }

    // Get the caller-supplied property values requested to be set on the object
    if (hr == S_OK)
    {
        hr = pParams->GetIPortableDeviceValuesValue(WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES, &pValues);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES");
    }

    // CoCreate a collection to store the property set operation results.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pWriteResults);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceValues");
    }

    // Set the property values on the specified object
    if (hr == S_OK)
    {
        // Since this driver does not support setting any properties, all property set operation
        // results will be set to E_ACCESSDENIED.
        if (hr == S_OK)
        {
            hr = pValues->GetCount(&cValues);
            CHECK_HR(hr, "Failed to get total number of values");
        }

        if (hr == S_OK)
        {
            for (DWORD dwIndex = 0; dwIndex < cValues; dwIndex++)
            {
                PROPERTYKEY Key = WPD_PROPERTY_NULL;
                hr = pValues->GetAt(dwIndex, &Key, NULL);
                CHECK_HR(hr, "Failed to get PROPERTYKEY at index %d", dwIndex);

                if (hr == S_OK)
                {
                    hr = pWriteResults->SetErrorValue(Key, E_ACCESSDENIED);
                    CHECK_HR(hr, "Failed to set error result value at index %d", dwIndex);
                }
            }
        }

        // Since we have set failures for the property set operations we must let the application
        // know by returning S_FALSE. This will instruct the application to look at the
        // property set operation results for failure values.
        if (hr == S_OK)
        {
            hr = S_FALSE;
        }
    }

    if (SUCCEEDED(hr))
    {
        // Set the WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_WRITE_RESULTS value in the results
        HRESULT hrTemp = pResults->SetIPortableDeviceValuesValue(WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_WRITE_RESULTS, pWriteResults);
        CHECK_HR(hrTemp, ("Failed to set WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_WRITE_RESULTS"));

        if (FAILED(hrTemp))
        {
            hr = hrTemp;
        }
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszObjectID);

    return hr;
}
```

 

 





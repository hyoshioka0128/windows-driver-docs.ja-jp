---
Description: プロパティ値の取得
title: プロパティ値の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab9ceae3b642ececd2ad222bf9f2a3dbfd12f3db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376232"
---
# <a name="property-value-retrieval"></a>プロパティ値の取得


WPD アプリケーションを呼び出すと、 **IPortableDeviceProperties::GetValues**メソッドでは、このメソッドは、さらに、いずれかへの呼び出しをトリガー、 **WpdObjectProperties::OnGetPropertyValues**または、 **WpdObjectProperties::OnGetAllPropertyValues**サンプル ドライバーでのメソッド。 場合、後者のメソッドが呼び出されます、2 番目の引数**IPortableDeviceProperties::GetValues**は**NULL**します。 サンプル ドライバーでこれらのメソッドを作成、 **IPortableDeviceValues**にドライバーが要求されたプロパティのプロパティ値を格納するオブジェクト。 サンプル ドライバーから次の例にはコードが含まれています、 **WpdObjectProperties::OnGetPropertyValues**メソッド。

```ManagedCPlusPlus
HRESULT WpdObjectProperties::OnGetPropertyValues(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr          = S_OK;
    LPWSTR  wszObjectID = NULL;
    CComPtr<IPortableDeviceValues>        pValues;
    CComPtr<IPortableDeviceKeyCollection> pKeys;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the object identifier whose property values have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID, &wszObjectID);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID");
    }

    // Get the list of property keys for the property values the caller wants to retrieve from the specified object
    if (hr == S_OK)
    {
        hr = pParams->GetIPortableDeviceKeyCollectionValue(WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_KEYS, &pKeys);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_KEYS");
    }

    // CoCreate a collection to store the property values.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pValues);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceValues");
    }

    // Read the specified properties on the specified object and add the property values to the collection.
    if (hr == S_OK)
    {
        hr = GetPropertyValuesForObject(wszObjectID, pKeys, pValues);
        CHECK_HR(hr, "Failed to get property values for object '%ws'", wszObjectID);
    }

    // S_OK or S_FALSE can be returned from GetPropertyValuesForObject( ).
    // S_FALSE means that 1 or more property values could not be retrieved successfully.
    // The value for the specified property should be set to an error HRESULT of
    // the reason why the property could not be read.
    // (e.g. If the property being requested is not supported on the object then an error of
    // HRESULT_FROM_WIN32(ERROR_NOT_SUPPORTED) should be set as the value.
    if (SUCCEEDED(hr))
    {
        // Set the WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES value in the results.
        HRESULT hrTemp = S_OK;
        hrTemp = pResults->SetIPortableDeviceValuesValue(WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES, pValues);
        CHECK_HR(hrTemp, ("Failed to set WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES"));

        if(FAILED(hrTemp))
        {
            hr = hrTemp;
        }
    }
```

 

 





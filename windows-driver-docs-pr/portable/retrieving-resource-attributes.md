---
Description: リソース属性の取得
title: リソース属性の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2df0c06a25c298f8bb1fcd8fff03547c86d7cde1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376229"
---
# <a name="retrieving-resource-attributes"></a>リソース属性の取得


呼び出しをアプリケーションが特定のリソースでサポートされている属性の一覧を取得する必要があるときに、 **IPortableDeviceResources::GetResourceAttributes**メソッドの識別子を指定する文字列を渡すと、対象となるリソースです。 この API 呼び出しをさらに、トリガー、 **WpdObjectResources::OnGetResourceAttributes**サンプル ドライバーでコマンド ハンドラー。 このメソッドを作成、 **IPortableDeviceValues**オブジェクトがリソースでサポートされている各属性の PROPERTYKEY/PROPVARIANT ペアが挿入されます。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnGetResourceAttributes(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT     hr          = S_OK;
    LPWSTR      wszObjectID = NULL;
    PROPERTYKEY Key         = WPD_PROPERTY_NULL;
    CComPtr<IPortableDeviceValues>  pAttributes;

    if (hr == S_OK)
    {
        hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID, &wszObjectID);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID");
    }

    if (hr == S_OK)
    {
        hr = pParams->GetKeyValue(WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS, &Key);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS");
    }

    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pAttributes);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceValues");
    }

    if (hr == S_OK)
    {
        hr = GetResourceAttributesForObject(wszObjectID, Key, pAttributes);
        CHECK_HR(hr, "Failed to get resource attributes");
    }

    if (SUCCEEDED(hr))
    {
        HRESULT hrTemp = S_OK;

        hrTemp = pResults->SetIPortableDeviceValuesValue(WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_ATTRIBUTES, pAttributes);
        CHECK_HR(hrTemp, ("Failed to set WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_ATTRIBUTES"));

        if(FAILED(hrTemp))
        {
            hr = hrTemp;
        }
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszObjectID);

    return hr;
}
```

 

 





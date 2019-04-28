---
Description: サポートされているリソース一覧の取得
title: サポートされているリソース一覧の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98ff05f45b7dfb4c46fe67a5f9c761453c43e0ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376227"
---
# <a name="retrieving-a-list-of-supported-resources"></a>サポートされているリソース一覧の取得


呼び出すことが、アプリケーションは、指定したオブジェクトでサポートされているリソースの一覧を取得する必要がある、ときに、 **IPortableDeviceResources::GetSupportedResources**メソッドとオブジェクトの識別子を指定する文字列を渡す該当します。 この API 呼び出しをさらに、トリガー、 **WpdObjectResources::OnGetSupportedResources**サンプル ドライバーでコマンド ハンドラー。 このメソッドを作成、 **IPortableDeviceKeyCollection**コマンド オブジェクトでサポートされている各リソースの PROPERTYKEY 値にコピーします。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnGetSupportedResources(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{

    HRESULT hr           = S_OK;
    LPWSTR  wszObjectID  = NULL;

    CComPtr<IPortableDeviceKeyCollection> pKeys;

    // Get the Object ID
    hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID, &wszObjectID);
    if (hr != S_OK)
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID");
    }

    // Create the collection to hold the resource keys
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceKeyCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceKeyCollection,
                              (VOID**) &pKeys);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceKeyCollection");
    }

    if (hr == S_OK)
    {
        hr = GetSupportedResourcesForObject(wszObjectID, pKeys);
        CHECK_HR(hr, "Failed to get supported resources for object '%ws'", wszObjectID);
    }

    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS, pKeys);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS");
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszObjectID);

    return hr;
}
```

 

 





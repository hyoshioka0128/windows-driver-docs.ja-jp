---
Description: Retrieving a list of Supported Resources
title: サポートされているリソースの一覧を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ab63133e01dd7f92e0dfacde51973b336966e8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549623"
---
# <a name="retrieving-a-list-of-supported-resources"></a>サポートされているリソースの一覧を取得します。


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
        CHECK_HR(hr, "Failed to get supported resources for object &#39;%ws&#39;", wszObjectID);
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

 

 





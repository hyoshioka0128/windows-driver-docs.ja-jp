---
Description: Mapping Object Identifiers
title: オブジェクト Id の割り当てください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d2edebc8fbd0ff7704cdb47c2d68d942d0f543
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548677"
---
# <a name="mapping-object-identifiers"></a>オブジェクト Id の割り当てください。


マッピング関数**WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs**、永続的な識別子にオブジェクト識別子のマッピングを処理します。 WPD ドライバー モデルでは、オブジェクト識別子は、特定のデバイスのセッションの有効なのみ識別子です。 永続的な識別子は、すべてのデバイス セッション間で有効です。

次のサンプル ドライバーからの抜粋のコードを含む**WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs します。**

```ManagedCPlusPlus
HRESULT WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs(
    IPortableDeviceValues* pParams,
    IPortableDeviceValues* pResults)
{

    HRESULT hr      = S_OK;
    DWORD   dwCount = 0;
    CComPtr<IPortableDevicePropVariantCollection> pPersistentIDs;
    CComPtr<IPortableDevicePropVariantCollection> pObjectIDs;

    if((pParams    == NULL) ||
       (pResults   == NULL))
    {
        hr = E_POINTER;
        CHECK_HR(hr, "Cannot have NULL parameter");
        return hr;
    }

    // Get the list of Persistent IDs
    if (hr == S_OK)
    {
        hr = pParams->GetIPortableDevicePropVariantCollectionValue(WPD_PROPERTY_COMMON_PERSISTENT_UNIQUE_IDS, &pPersistentIDs);
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_PERSISTENT_UNIQUE_IDS");
    }

    // Create the collection to hold the ObjectIDs
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pObjectIDs);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Iterate through the persistent ID list and add the equivalent object ID for each element.
    if (hr == S_OK)
    {
        hr = pPersistentIDs->GetCount(&dwCount);
        CHECK_HR(hr, "Failed to get count from persistent ID collection");

        if (hr == S_OK)
        {
            DWORD       dwIndex        = 0;
            PROPVARIANT pvPersistentID = {0};
            PROPVARIANT pvObjectID     = {0};

            PropVariantInit(&pvPersistentID);
            PropVariantInit(&pvObjectID);

            for(dwIndex = 0; dwIndex < dwCount; dwIndex++)
            {
                pvObjectID.vt = VT_LPWSTR;
                hr = pPersistentIDs->GetAt(dwIndex, &pvPersistentID);
                CHECK_HR(hr, "Failed to get persistent ID at index %d", dwIndex);

                // Because our persistent unique identifiers are identical to our object
                // identifiers, we just return it back to the caller.
                if (hr == S_OK)
                {
                    pvObjectID.pwszVal = AtlAllocTaskWideString(pvPersistentID.pwszVal);
                }

                if (hr == S_OK)
                {
                    hr = pObjectIDs->Add(&pvObjectID);
                    CHECK_HR(hr, "Failed to add next Object ID");
                }

                PropVariantClear(&pvPersistentID);
                PropVariantClear(&pvObjectID);

                if(FAILED(hr))
                {
                    break;
                }
            }
        }
    }

    if (hr == S_OK)
    {
        hr = pResults->SetIPortableDevicePropVariantCollectionValue(WPD_PROPERTY_COMMON_OBJECT_IDS, pObjectIDs);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_COMMON_OBJECT_IDS");
    }

    return hr;
}
```

一部のデバイスは、オブジェクトに永続的な識別子を格納する場合があります、いくつかオブジェクトのデータのハッシュに基づいて永続的な識別子を生成する可能性があります (これらは変更されません) ために、永続的な識別子としてそれらのオブジェクト識別子を扱う他のユーザー可能性があります。 WpdHelloWorldDriver サンプルでは、この後者の場合を実装します。

クライアント アプリケーションを呼び出すと、 **IPortableDeviceContent::GetObjectIDsFromPersistentUniqueIDs** 、ドライバー、メソッドが呼び出されます、 **WpdBaseDriver::OnGetObjectIDsFromPersistentUniqueIDs**.

 

 





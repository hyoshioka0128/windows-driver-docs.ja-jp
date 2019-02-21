---
Description: Reading Resource Data
title: リソース データの読み取り
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c50ef5912266fdb8420ee0edf9aaea2ed3b0b8cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529631"
---
# <a name="reading-resource-data"></a>リソース データの読み取り


アプリケーションが取得された後、 **IStream**オブジェクトの場合、必要な読み取りを実行またはを使用して操作を書き込むことができます、 **:read**または**IStream::Write**メソッド。 (サンプル ドライバーの場合読み取り操作のみサポートされます)。 アプリケーションを呼び出すと、 **:read**メソッドでは、このメソッドは、さらに、デバイス ドライバーへの呼び出しをトリガー **WpdObjectResources::OnReadResource**メソッドで、実際の読み取りを実行します。操作です。

**WpdObjectResources::OnReadResource**メソッドは、コピー先のバッファーに要求されたバイト数を読み取ります、転送されたバイトの数は、リソースのコンテキストを更新します。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnReadResource(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT                   hr                 = S_OK;
    LPWSTR                    wszResourceContext = NULL;
    DWORD                     dwNumBytesToRead   = 0;
    DWORD                     dwNumBytesRead     = 0;
    BYTE*                     pBuffer            = NULL;
    DWORD                     cbBuffer           = 0;
    WpdObjectResourceContext* pResourceContext   = NULL;
    ContextMap*               pContextMap        = NULL;

    // Get the enumeration context identifier for this enumeration operation.  We will
    // need this to look up the specific enumeration context in the client context map.
    hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT, &wszResourceContext);
    if (hr != S_OK)
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT");
    }

    // Get the number of bytes to read
    if (hr == S_OK)
    {
        hr = pParams->GetUnsignedIntegerValue(WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_TO_READ, &dwNumBytesToRead);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_TO_READ");
    }

    // Get the destination buffer
    if (hr == S_OK)
    {
        hr = pParams->GetBufferValue(WPD_PROPERTY_OBJECT_RESOURCES_DATA, &pBuffer, &cbBuffer);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_DATA");
    }

    // Get the client context map so we can retrieve the resource context for this resource
    // operation using the WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT property value obtained above.
    if (hr == S_OK)
    {
        hr = pParams->GetIUnknownValue(PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP, (IUnknown**)&pContextMap);
        CHECK_HR(hr, "Failed to get PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP");
    }

    if (hr == S_OK)
    {
        pResourceContext = (WpdObjectResourceContext*)pContextMap->GetContext(wszResourceContext);
        if (pResourceContext == NULL)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "Missing resource context");
        }
    }

    // Read the next chunk of data for this request
    if (hr == S_OK)
    {
        hr = ReadDataFromResource(pResourceContext, pBuffer, dwNumBytesToRead, &dwNumBytesRead);
        CHECK_HR(hr, "Failed to read %d bytes from resource", dwNumBytesToRead);
    }

    if (hr == S_OK)
    {
        hr = pResults->SetBufferValue(WPD_PROPERTY_OBJECT_RESOURCES_DATA, pBuffer, dwNumBytesRead);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_OBJECT_RESOURCES_DATA");
    }

    if (hr == S_OK)
    {
        hr = pResults->SetUnsignedIntegerValue(WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_READ, dwNumBytesRead);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_READ");
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszResourceContext);

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(pBuffer);

    SAFE_RELEASE(pContextMap);

    return hr;
}
```

 

 





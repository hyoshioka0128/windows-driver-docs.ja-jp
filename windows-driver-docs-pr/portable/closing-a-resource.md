---
Description: Closing a Resource
title: リソースを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338a3dc252b900fe66163ba75dbf6c69ad146924
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558889"
---
# <a name="closing-a-resource"></a>リソースを閉じる


アプリケーションを使用して、読み取りまたは書き込み操作が完了した後、指定された**IStream**オブジェクトを呼び出すことによって、ストリームを閉じ、 **IStream::Release**または**IStream::Commit**(を保存するリソースの変更書き込み要求)。 アプリケーション レベルのトリガーで終了要求、 **WpdObjectResources::OnCloseResource**ドライバーのメソッド。

主な仕事、 **WpdObjectResources::OnCloseResource**クライアント コンテキスト マップから、リソースのコンテキスト データを削除し、関連付けられているメモリを解放する方法です。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnCloseResource(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT     hr                 = S_OK;
    LPWSTR      wszResourceContext = NULL;
    ContextMap* pContextMap        = NULL;

    UNREFERENCED_PARAMETER(pResults);

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the resource context identifier for this resource operation.  We will
    // need this to look up the specific resource context in the client context map.
    hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT, &wszResourceContext);
    if (hr != S_OK)
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT");
    }

    // Get the client context map so we can retrieve the resource context for this resource
    // operation by using the WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT property value obtained previously.
    if (hr == S_OK)
    {
        hr = pParams->GetIUnknownValue(PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP, (IUnknown**)&pContextMap);
        CHECK_HR(hr, "Failed to get PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP");
    }

    // Destroy any data, either allocated or associated, with the resource context and then remove it from the context map.
    // We no longer need to keep this context around because the resource operation has ended.
    if (hr == S_OK)
    {
        pContextMap->Remove(wszResourceContext);
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszResourceContext);

    SAFE_RELEASE(pContextMap);

    return hr;
}
```

 

 





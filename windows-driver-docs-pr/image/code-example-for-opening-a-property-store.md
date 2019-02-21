---
title: プロパティ ストアを開くためのコード例
description: プロパティ ストアを開くためのコード例
ms.assetid: 4d63ea52-f3f5-4af7-ad6f-0bbd57b76c52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8089fd1fb13593362c4cff35ddaa9427125ce3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551926"
---
# <a name="code-example-for-opening-a-property-store"></a>プロパティ ストアを開くためのコード例


次のコード例では、現在の関数インスタンス オブジェクトのプロパティ ストアを開く方法を示します。 現在の関数インスタンス オブジェクトを取得するための手順で説明されて[関数インスタンスのオブジェクトを取得する](obtaining-a-function-instance-object.md)します。

```cpp
/**************************************************************************\
* CWSDDevice::OpenPropertyStore
*
* Opens the Property Store that is associated with the current Function Instance. 
*
* Arguments:
*
*    pPropertyStore - returns the IPropertyStore interface. The caller must
*                     release it by calling IPropertyStore::Release
* Return Value:
*
*     S_OK if operation is successful, an error HRESULT otherwise
*
\**************************************************************************/

HRESULT
CWSDDevice::OpenPropertyStore(
    __out IPropertyStore **ppPropertyStore)
{
    HRESULT hr = S_OK;

    if (!ppPropertyStore)
    {
        hr = E_INVALIDARG;
        WIAS_ERROR((g_hInst, "Invalid argument, hr = 0x%08X", hr));
    }

    if (!m_pFunctionInstance)
    {
        hr = E_UNEXPECTED;
        WIAS_ERROR((g_hInst, "Communication interface not initialized, hr = 0x%08X", hr));
    }

    if (SUCCEEDED(hr))
    {
        hr = m_pFunctionInstance->OpenPropertyStore(STGM_READ, ppPropertyStore);
        if ((SUCCEEDED(hr)) && (!(*ppPropertyStore)))
        {
            hr = E_POINTER;
            WIAS_ERROR((g_hInst, 
                "IFunctionInstance::OpenPropertyStore returned hr = 0x%08X with a NULL property store interface, hr = 0x%08X", hr));
        }
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "IFunctionInstance::OpenPropertyStore failed, hr = 0x%08X", hr));
        }
    }

    return hr;
}
```

 

 





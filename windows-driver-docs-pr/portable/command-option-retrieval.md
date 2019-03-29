---
Description: コマンドオプションの取得
title: コマンドオプションの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fdeca565a37e86ad21543b95badb75cf0246e3
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349921"
---
# <a name="command-option-retrieval"></a>コマンドオプションの取得


WPD アプリケーションを呼び出すと、 **IPortableDeviceCapabilities::GetCommandOptions**メソッドでは、このメソッドは、さらへの呼び出しをトリガー、 **WpdCapabilities::OnGetCommandOptions**サンプル メソッドドライバー。 後者のメソッドを作成、 **IPortableDeviceValues**にドライバーが格納オブジェクトがサポートされているオプション。 ドライバーのサンプルでは、コマンドのオプションはサポートされていません、このメソッドによって返されるコレクションは空です。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetCommandOptions(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT     hr      = S_OK;
    PROPERTYKEY Command = WPD_PROPERTY_NULL;
    CComPtr<IPortableDeviceValues> pOptions;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the command whose options have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetKeyValue(WPD_PROPERTY_CAPABILITIES_COMMAND, &Command);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_COMMAND");
    }

    // CoCreate a collection to store the command options.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pOptions);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValues");
    }

    // Add command options to the collection
    if (hr == S_OK)
    {
        // If your driver supports command options, then they should be added here
        // to the command options collection 'pOptions'.
    }

    // Set the WPD_PROPERTY_CAPABILITIES_COMMAND_OPTIONS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_COMMAND_OPTIONS, pOptions);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_COMMAND_OPTIONS");
    }

    return hr;
}
```

 

 





---
Description: Supported Command Retrieval
title: サポートされているコマンドの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee426cc7ae542818325e98cbf3411e368f2270a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528377"
---
# <a name="supported-command-retrieval"></a>サポートされているコマンドの取得


WPD アプリケーションを呼び出すと、 **IPortableDeviceCapabilities::GetSupportedCommands**メソッドでは、このメソッドは、さらへの呼び出しをトリガー、 **WpdCapabilities::OnGetSupportedCommands**メソッドで、ドライバーのサンプルです。 後者のメソッドを作成、 **IPortableDeviceKeyCollection**ドライバーをサポートしているコマンドの一覧が格納オブジェクト。 場合は、サンプル ドライバーでは、22 のサポートされているコマンドには 4 つのカテゴリです。

```ManagedCPlusPlus
const PROPERTYKEY g_SupportedCommands[] =
{
    // WPD_CATEGORY_OBJECT_ENUMERATION
    WPD_COMMAND_OBJECT_ENUMERATION_START_FIND,
    WPD_COMMAND_OBJECT_ENUMERATION_FIND_NEXT,
    WPD_COMMAND_OBJECT_ENUMERATION_END_FIND,

    // WPD_CATEGORY_OBJECT_PROPERTIES
    WPD_COMMAND_OBJECT_PROPERTIES_GET_SUPPORTED,
    WPD_COMMAND_OBJECT_PROPERTIES_GET,
    WPD_COMMAND_OBJECT_PROPERTIES_GET_ALL,
    WPD_COMMAND_OBJECT_PROPERTIES_SET,
    WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES,
    WPD_COMMAND_OBJECT_PROPERTIES_DELETE,

    // WPD_CATEGORY_OBJECT_RESOURCES
    WPD_COMMAND_OBJECT_RESOURCES_GET_SUPPORTED,
    WPD_COMMAND_OBJECT_RESOURCES_OPEN,
    WPD_COMMAND_OBJECT_RESOURCES_READ,
    WPD_COMMAND_OBJECT_RESOURCES_CLOSE,
    WPD_COMMAND_OBJECT_RESOURCES_GET_ATTRIBUTES,

    // WPD_CATEGORY_CAPABILITIES
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS,
    WPD_COMMAND_CAPABILITIES_GET_COMMAND_OPTIONS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES,
    WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_CONTENT_TYPES,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMATS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMAT_PROPERTIES,
    WPD_COMMAND_CAPABILITIES_GET_FIXED_PROPERTY_ATTRIBUTES,
};
```

次の抜粋、 *WpdCapabilities.cpp*ファイルにはコードが含まれています、 **OnGetSupportedCommands**メソッド。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetSupportedCommands(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDeviceKeyCollection> pCommands;
    UNREFERENCED_PARAMETER(pParams);

    // CoCreate a collection to store the supported commands.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceKeyCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceKeyCollection,
                              (VOID**) &pCommands);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceKeyCollection");
    }

    // Add the supported commands to the collection.
    if (hr == S_OK)
    {
        for (DWORD dwIndex = 0; dwIndex < ARRAYSIZE(g_SupportedCommands); dwIndex++)
        {
            hr = pCommands->Add(g_SupportedCommands[dwIndex]);
            CHECK_HR(hr, "Failed to add supported command at index %d", dwIndex);
            if (FAILED(hr))
            {
                break;
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_SUPPORTED_COMMANDS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_SUPPORTED_COMMANDS, pCommands);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_SUPPORTED_COMMANDS");
    }

    return hr;
}
```

 

 





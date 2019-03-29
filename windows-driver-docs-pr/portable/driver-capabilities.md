---
Description: Driver Capabilities
title: ドライバーの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5616504930a48c3c1f0dfc72deb75ee432e8d460
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571329"
---
# <a name="driver-capabilities"></a>ドライバーの機能


*WpdCapabilities.cpp*と*WpdCapabilities.h*ファイルには、サポートされているコマンド、コマンド オプション、関数のカテゴリを取得するコマンド ハンドラーが含まれています。

Windows ベースのアプリケーションを呼び出すメソッドのいずれかと、 **IPortableDeviceCapabilities**インターフェイスでは、この呼び出しをさらに、トリガーで 8 つのコマンド ハンドラーの 1 つ、 **WpdCapabilities**クラス。 次の表のマッピングを識別する**IPortableDeviceCapabilities**メソッド**WpdCapabilities**コマンド ハンドラー。

|                                                               |                                    |
|---------------------------------------------------------------|------------------------------------|
| **IPortableDeviceCapabilities メソッド**                        | **WpdCapabilities イベント ハンドラー**  |
| **IPortableDeviceCapabilities::GetCommandOptions**            | **OnGetCommandOptions**            |
| **IPortableDeviceCapabilities::GetFixedPropertyAttributes**   | **OnGetFixedPropertyAttributes**   |
| **IPortableDeviceCapabilities::GetFunctionalCategories**      | **OnGetFunctionalCategories**      |
| **IPortableDeviceCapabilities::GetFunctionalObjects**         | **OnGetFunctionalObjects**         |
| **IPortableDeviceCapabilities::GetSupportedCommands**         | **OnGetSupportedCommands**         |
| **IPortableDeviceCapabilities::GetSupportedContentTypes**     | **OnGetSupportedContentTypes**     |
| **IPortableDeviceCapabilities::GetSupportedFormatProperties** | **OnGetSupportedFormatProperties** |
| **IPortableDeviceCapabilities::GetSupportedFormats**          | **OnGetSupportedFormats**          |
| **IPortableDeviceCapabilities::GetSupportedEvents**           | **OnGetSupportedEvents**           |
| **IPortableDeviceCapabilities::GetEventOptions**              | **OnGetEventOptions**              |

 

によって WpdCapabilities コマンド ハンドラーが呼び出される、 **WpdCapabilities::DispatchMessage**メソッド。 次のサンプル ドライバーからの抜粋のコードを含む**WpdCapabilities::DispatchMessage**します。

```ManagedCPlusPlus
HRESULT WpdCapabilities::DispatchWpdMessage(const PROPERTYKEY&      Command,
                                            IPortableDeviceValues*  pParams,
                                            IPortableDeviceValues*  pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_CAPABILITIES)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS))
        {
            hr = OnGetSupportedCommands(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported commands");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_COMMAND_OPTIONS))
        {
            hr = OnGetCommandOptions(pParams, pResults);
            CHECK_HR(hr, "Failed to get command options");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES))
        {
            hr = OnGetFunctionalCategories(pParams, pResults);
            CHECK_HR(hr, "Failed to get functional categories");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS))
        {
            hr = OnGetFunctionalObjects(pParams, pResults);
            CHECK_HR(hr, "Failed to get functional objects");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_CONTENT_TYPES))
        {
            hr = OnGetSupportedContentTypes(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported content types");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMATS))
        {
            hr = OnGetSupportedFormats(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported formats");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMAT_PROPERTIES))
        {
            hr = OnGetSupportedFormatProperties(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported format properties");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_FIXED_PROPERTY_ATTRIBUTES))
        {
            hr = OnGetFixedPropertyAttributes(pParams, pResults);
            CHECK_HR(hr, "Failed to get fixed property attributes");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_EVENTS))
        {
            hr = OnGetSupportedEvents(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported events");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_EVENT_OPTIONS))
        {
            hr = OnGetEventOptions(pParams, pResults);
            CHECK_HR(hr, "Failed to get event options");
        }
        else
        {
            hr = E_NOTIMPL;
            CHECK_HR(hr, "This object does not support this command id %d", Command.pid);
        }
    }
    return hr;
}
```

 

 





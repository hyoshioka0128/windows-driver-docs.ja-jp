---
Description: ドライバーの機能
title: ドライバーの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd4e0ef946c35f2b8a6cb29f7c44033db4cbf2f2
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968585"
---
# <a name="driver-capabilities"></a>ドライバーの機能


*Wpdcapabilities .cpp*および*wpdcapabilities .h*ファイルには、サポートされているコマンド、コマンドオプション、関数カテゴリなどを取得するコマンドハンドラーが含まれています。

Windows ベースのアプリケーションが**IPortableDeviceCapabilities**インターフェイスのメソッドのいずれかを呼び出すと、この呼び出しは**wpdcapabilities**クラスの8つのコマンドハンドラーの1つをトリガーします。 次の表は、 **IPortableDeviceCapabilities**メソッドから**wpdcapabilities**コマンドハンドラーへのマッピングを示しています。

IPortableDeviceCapabilities メソッド * * * *: **Wpdcapabilities イベントハンドラー**

IPortableDeviceCapabilities:: GetCommandOptions * * * *: **OnGetCommandOptions**

IPortableDeviceCapabilities:: GetFixedPropertyAttributes * * * *: **OnGetFixedPropertyAttributes**

IPortableDeviceCapabilities:: GetFunctionalCategories * * * *: **OnGetFunctionalCategories**

IPortableDeviceCapabilities:: GetFunctionalObjects * * * *: **OnGetFunctionalObjects**

IPortableDeviceCapabilities:: GetSupportedCommands * * * *: **OnGetSupportedCommands**

IPortableDeviceCapabilities:: GetSupportedContentTypes * * * *: **OnGetSupportedContentTypes**

IPortableDeviceCapabilities:: GetSupportedFormatProperties * * * *: **OnGetSupportedFormatProperties**

IPortableDeviceCapabilities:: GetSupportedFormats * * * *: **OnGetSupportedFormats**

IPortableDeviceCapabilities:: GetSupportedEvents * * * *: **OnGetSupportedEvents**

IPortableDeviceCapabilities:: GetEventOptions * * * *: **OnGetEventOptions**


 

WpdCapabilities コマンドハンドラーは、 **wpdcapabilities::D ispatchmessage**メソッドによって呼び出されます。 サンプルドライバーの次の抜粋には、 **Wpdcapabilities**のコード (:D ispatchmessage) が含まれています。

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

 

 





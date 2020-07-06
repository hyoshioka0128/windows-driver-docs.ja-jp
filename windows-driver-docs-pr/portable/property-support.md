---
Description: プロパティのサポート
title: プロパティのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 445700819101499437251fbaff795a6730994a74
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967859"
---
# <a name="property-support"></a>プロパティのサポート


*WpdObjectProperties*ファイルと*WpdObjectProperties*ファイルには、デバイスのオブジェクトプロパティを設定および取得するメンバー関数が含まれています。

Windows アプリケーションが**Iportabledeviceproperties**インターフェイスの5つのメソッドのいずれかを呼び出すと、この呼び出しによって**WpdObjectProperty**クラスの5つのコマンドハンドラーのいずれかがトリガーされます。 次の表は、 **WpdObjectProperties** driver メソッドへのアプリケーションメソッドのマッピングを示しています。

IPortableDeviceProperties メソッド * * * *: **WpdObjectProperties コマンドハンドラー**

IPortableDeviceProperties::D e) * * * *: **OnDelete**

IPortableDeviceProperties:: GetPropertyAttributes * * * *: **OnGetPropertyAttributes**

IPortableDeviceProperties:: GetSupportedProperties * * * *: **OnGetSupportedProperties**

IPortableDeviceProperties:: GetValues * * * *: **OnGetPropertyValues または OnGetAllPropertyValues**

IPortableDeviceProperties:: SetValues * * * *: **OnSetPropertyValues**


 

WpdObjectProperties コマンドハンドラーは、 **WpdObjectProperty::D ispatchwpdmessage**メソッドによって呼び出されます。 サンプルドライバーの次の抜粋には、 **WpdObjectProperty::D ispatchwpdmessage**のコードが含まれています。

```ManagedCPlusPlus
HRESULT WpdObjectProperties::DispatchWpdMessage(
    const PROPERTYKEY&     Command,
    IPortableDeviceValues* pParams,
    IPortableDeviceValues* pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_OBJECT_PROPERTIES)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET_SUPPORTED))
        {
            hr = OnGetSupportedProperties(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported properties");
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET))
        {
            hr = OnGetPropertyValues(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get properties");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET_ALL))
        {
            hr = OnGetAllPropertyValues(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get all properties");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_SET))
        {
            hr = OnSetPropertyValues(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to set properties");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES))
        {
            hr = OnGetPropertyAttributes(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get property attributes");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_DELETE))
        {
            hr = OnDeleteProperties(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to delete properties");
            }
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

 

 





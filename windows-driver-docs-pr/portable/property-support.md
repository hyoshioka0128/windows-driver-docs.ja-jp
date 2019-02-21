---
Description: Property Support
title: プロパティのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a36aaa31b751f6672e97906fe6d8aa6c90e9e8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535933"
---
# <a name="property-support"></a>プロパティのサポート


*WpdObjectProperties.cpp*と*WpdObjectProperties.h*ファイルには設定し、デバイス上のオブジェクトのプロパティを取得するメンバー関数が含まれます。

Windows アプリケーションを呼び出すには、5 つのメソッドのいずれかと、 **IPortableDeviceProperties**インターフェイスでは、この呼び出しをさらに、トリガーで 5 つのコマンド ハンドラーの 1 つ、 **WpdObjectProperty**クラス。 次の表に、アプリケーション メソッドのマッピング**WpdObjectProperties**ドライバー メソッド。

|                                                       |                                                   |
|-------------------------------------------------------|---------------------------------------------------|
| **IPortableDeviceProperties メソッド**                  | **WpdObjectProperties コマンド ハンドラー**           |
| **IPortableDeviceProperties::Delete**                 | **OnDelete**                                      |
| **IPortableDeviceProperties::GetPropertyAttributes**  | **OnGetPropertyAttributes**                       |
| **IPortableDeviceProperties::GetSupportedProperties** | **OnGetSupportedProperties**                      |
| **IPortableDeviceProperties::GetValues**              | **OnGetPropertyValues または OnGetAllPropertyValues** |
| **IPortableDeviceProperties::SetValues**              | **OnSetPropertyValues**                           |

 

によって WpdObjectProperties コマンド ハンドラーが呼び出される、 **WpdObjectProperty::DispatchWpdMessage**メソッド。 次のサンプル ドライバーからの抜粋のコードを含む**WpdObjectProperty::DispatchWpdMessage:**

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

 

 





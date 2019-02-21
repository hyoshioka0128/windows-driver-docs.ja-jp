---
Description: Messaging Functionality
title: メッセージングの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa1d8d1c8f854bec2a99d6af4a2347f720c53990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527978"
---
# <a name="messaging-functionality"></a>メッセージングの機能


メッセージングの関数では、 **WpdBaseDriver::DispatchWpdMessage**、適切なドライバー コンポーネントへのメッセージの配布を処理します。 前に Windows のプログラムを作成した場合の考えることができます、 **DispatchWpdMessage**同様の Windows ベースのアプリケーションの役目を果たす**WindowProc**関数。

**WpdBaseDriver::DispatchWpdMessage**関数は、WPD\_コマンドの分類を特定のメッセージを送信します。 次に、適切なコンポーネント (列挙型、プロパティ、リソース、または機能コンポーネント、ドライバーに) には、このメッセージを渡します。

*PParams*引数が指す、 **IPortableDeviceValues**特定コマンドのパラメーターを逆シリアル化を含むコレクション。

*PResults*の空のコレクションを指す引数**IPortableDeviceValues**処理が指定されたコマンドの後に、関数が作成されます。

次のサンプル ドライバーからの抜粋のコードを含む**WpdBaseDriver::DispatchWpdMessage します。**

```ManagedCPlusPlus
HRESULT WpdBaseDriver::DispatchWpdMessage(IPortableDeviceValues* pParams,
                                          IPortableDeviceValues* pResults)
{

    HRESULT     hr                  = S_OK;
    GUID        guidCommandCategory = {0};
    DWORD       dwCommandID         = 0;
    PROPERTYKEY CommandKey          = WPD_PROPERTY_NULL;

    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_COMMON_COMMAND_CATEGORY, &guidCommandCategory);
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_COMMAND_CATEGORY from input parameters");
    }

    if (hr == S_OK)
    {
        hr = pParams->GetUnsignedIntegerValue(WPD_PROPERTY_COMMON_COMMAND_ID, &dwCommandID);
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_COMMAND_ID from input parameters");
    }

    // If WPD_PROPERTY_COMMON_COMMAND_CATEGORY or WPD_PROPERTY_COMMON_COMMAND_ID could not be extracted
    // properly then we should return E_INVALIDARG to the client.
    if (FAILED(hr))
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_COMMAND_CATEGORY or WPD_PROPERTY_COMMON_COMMAND_ID from input parameters");
    }

    if (hr == S_OK)
    {
        CommandKey.fmtid = guidCommandCategory;
        CommandKey.pid   = dwCommandID;

        if (CommandKey.fmtid == WPD_CATEGORY_OBJECT_ENUMERATION)
        {
            hr = m_ObjectEnum.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (CommandKey.fmtid == WPD_CATEGORY_OBJECT_PROPERTIES)
        {
            hr = m_ObjectProperties.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (CommandKey.fmtid == WPD_CATEGORY_OBJECT_RESOURCES)
        {
            hr = m_ObjectResources.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (CommandKey.fmtid == WPD_CATEGORY_CAPABILITIES)
        {
            hr = m_Capabilities.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (IsEqualPropertyKey(CommandKey, WPD_COMMAND_COMMON_GET_OBJECT_IDS_FROM_PERSISTENT_UNIQUE_IDS))
        {
            hr = OnGetObjectIDsFromPersistentUniqueIDs(pParams, pResults);
        }
        else
        {
            hr = E_NOTIMPL;
            CHECK_HR(hr, "Unknown command %ws.%d received",CComBSTR(CommandKey.fmtid), CommandKey.pid);
        }
    }

    HRESULT hrTemp = pResults->SetErrorValue(WPD_PROPERTY_COMMON_HRESULT, hr);
    CHECK_HR(hrTemp, ("Failed to set WPD_PROPERTY_COMMON_HRESULT"));

    // Set to a success code, to indicate that the message was received.
    // the return code for the actual command&#39;s results is stored in the
    // WPD_PROPERTY_COMMON_HRESULT property.
    hr = S_OK;

    return hr;
}
```

 

 





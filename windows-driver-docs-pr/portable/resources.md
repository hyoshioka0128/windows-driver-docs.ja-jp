---
Description: 参考資料
title: 参考資料
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5baec576ec1941551f33e4962626cd1c13e5fbaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376215"
---
# <a name="resources"></a>参考資料


*WpdObjectResources.cpp*と*WpdObjectResources.h*ファイルには開くまたは特定のリソースを閉じて、リソースの内容を読み取り、いる属性を取得するメンバー関数が含まれますリソースでサポートされているし、特定のオブジェクトでサポートされているリソースを取得します。

サンプル ドライバーの場合は、ドキュメント フォルダー オブジェクト内に存在する 1 つのリソース (サンプルの readme のテキスト ファイル)。

Windows ベースのアプリケーションを呼び出すメソッドのいずれかと、 **IPortableDeviceResources**インターフェイスでは、この呼び出しをさらに、トリガー WpdObjectResources クラスでいくつかのコマンド ハンドラーの 1 つ。 次の表は、アプリケーション メソッド WpdObjectResource メソッドへのマッピングを識別します。

| WpdObjectResources コマンド ハンドラー           | 説明                                                                                                                            |
|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| WpdObjectResources::OnCloseResource          | 閉じる操作への応答と呼ばれる、 **IStream**オブジェクトを**OnOpenResource**が返されます。                                    |
| WpdObjectResources::OnGetResourceAttributes します。 | 呼び出し元アプリケーションへの応答と呼ばれる、 **IPortableDeviceResources::GetResourceAttributes**メソッド。                          |
| WpdObjectResources::OnGetSupportedResources  | 呼び出し元アプリケーションへの応答と呼ばれる、 **IPortableDeviceResources::GetSuportedResources**メソッド。                           |
| WpdObjectResources::OnOpenResource           | 呼び出し元アプリケーションへの応答と呼ばれる、 **IPortableDeviceResources::GetStream**メソッド。                                      |
| WpdObjectResources::OnReadResource           | 呼び出し元アプリケーションへの応答と呼ばれる、 **:read**メソッドを**IStream**オブジェクトを**OnOpenResource**が返されます。 |

 

によって WpdObjectResources コマンド ハンドラーが呼び出される、 **WpdObjectResources::DispatchWpdMessage**メソッド。 次のサンプル ドライバーからの抜粋のコードを含む**WpdObjectResources::DispatchWpdMessage**します。

```ManagedCPlusPlus
HRESULT WpdObjectResources::DispatchWpdMessage(
    const PROPERTYKEY&     Command,
    IPortableDeviceValues* pParams,
    IPortableDeviceValues* pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_OBJECT_RESOURCES)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_GET_SUPPORTED))
        {
            hr = OnGetSupportedResources(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported resources");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_OPEN))
        {
            hr = OnOpenResource(pParams, pResults);
            CHECK_HR(hr, "Failed to open resource");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_READ))
        {
            hr = OnReadResource(pParams, pResults);
            CHECK_HR(hr, "Failed to read resource");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_CLOSE))
        {
            hr = OnCloseResource(pParams, pResults);
            CHECK_HR(hr, "Failed to close resource");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_GET_ATTRIBUTES))
        {
            hr = OnGetResourceAttributes(pParams, pResults);
            CHECK_HR(hr, "Failed to get resource attributes");
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

 

 





---
Description: 機能のコマンド (WpdBasicHardwareDriver サンプル) のサポート
title: 機能のコマンド (WpdBasicHardwareDriver サンプル) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33c40f06cebbc17e6d45918cb502b4e4fc6b2930
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387300"
---
# <a name="support-for-capability-commands-wpdbasichardwaredriver-sample"></a>機能のコマンド (WpdBasicHardwareDriver サンプル) のサポート


ドライバーのサンプルでは、10 の機能のコマンドをサポートします。 これらのコマンドが最初に、処理、 **WpdCapabilities::DispatchMessage**メソッドを対応するコマンド ハンドラーが呼び出されます。 **DispatchMessage**メソッドと個別のハンドラーは、「、 *WpdCapabilities.cpp*ファイル。

次の表の情報を説明のプロパティがサポートされているコマンド ハンドラーの名前と各を**DispatchMessage**特定のコマンドを処理するときに呼び出します。

| コマンド                                                            | ハンドラー                        | 説明                                                                                                                                     |
|--------------------------------------------------------------------|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WPD\_コマンド\_機能\_取得\_サポートされている\_コマンド               | OnGetSupportedCommands         | アプリケーションがデバイスでサポートされているコマンドのセットを取得しようとしたときに発行されます。                                           |
| WPD\_コマンド\_機能\_取得\_コマンド\_オプション                  | OnGetCommandOptions            | アプリケーションが特定のコマンドでサポートされているオプションを取得しようとしたときに発行されます。                                              |
| WPD\_コマンド\_機能\_取得\_サポートされている\_機能\_カテゴリ | OnGetFunctionalCategories      | アプリケーションがデバイスでサポートされている機能のカテゴリのセットを取得しようとしたときに発行されます。                              |
| WPD\_コマンド\_機能\_取得\_機能\_オブジェクト               | OnGetFunctionalObjects         | アプリケーションが特定の機能カテゴリでサポートされている機能のオブジェクトのセットを取得しようとしたときに発行されます。                |
| WPD\_コマンド\_機能\_取得\_サポートされている\_コンテンツ\_型         | OnGetSupportedContentTypes     | アプリケーションが特定の機能カテゴリでサポートされているコンテンツの種類を取得しようとしたときに発行されます。                            |
| WPD\_コマンド\_機能\_取得\_サポートされている\_書式設定                | OnGetSupportedFormats          | アプリケーションが特定のコンテンツ タイプでサポートされている形式のセットを取得しようとしたときに発行されます。                                  |
| WPD\_コマンド\_機能\_取得\_サポートされている\_形式\_プロパティ     | OnGetSupportedFormatProperties | アプリケーションが特定の形式でサポートされているプロパティのセットを取得しようとしたときに発行されます。                                     |
| WPD\_コマンド\_機能\_取得\_固定\_プロパティ\_属性       | OnGetFixedPropertyAttributes   | アプリケーションが同じ (または固定) のプロパティ属性のセットを取得しようとしたときに発行された、特定形式のすべてのオブジェクト。 |
| WPD\_コマンド\_機能\_取得\_イベント\_オプション                    | OnGetEventOptions              | アプリケーションが特定のイベントに関連付けられているオプションを取得しようとしたときに発行されます。                                             |
| WPD\_コマンド\_機能\_取得\_サポートされている\_イベント                 | OnGetEventOptions              | アプリケーションがデバイスでサポートされているイベントのセットを取得しようとしたときに発行されます。                                               |

 

サンプル ドライバーの場合、コードは、次のコマンドに関連付けられているハンドラーをそのまま残っています。

-   WPD\_コマンド\_機能\_取得\_コマンド\_オプション
-   WPD\_コマンド\_機能\_取得\_サポートされている\_形式\_プロパティ
-   WPD\_コマンド\_機能\_取得\_固定\_プロパティ\_属性
-   WPD\_コマンド\_機能\_取得\_サポートされている\_形式\_プロパティ

ただし、次のハンドラーのコードが変更されました。

-   WPD\_コマンド\_機能\_取得\_サポートされている\_コマンド
-   WPD\_コマンド\_機能\_取得\_サポートされている\_機能\_カテゴリ
-   WPD\_コマンド\_機能\_取得\_機能\_オブジェクト
-   WPD\_コマンド\_機能\_取得\_サポートされている\_コンテンツ\_型
-   WPD\_コマンド\_機能\_取得\_サポートされている\_書式設定
-   WPD\_コマンド\_機能\_取得\_サポートされている\_イベント
-   WPD\_コマンド\_機能\_取得\_イベント\_オプション

## <a name="span-idwpdcommandcapabilitiesgetsupportedcommandsspanspan-idwpdcommandcapabilitiesgetsupportedcommandsspanwpdcommandcapabilitiesgetsupportedcommands"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS"></span><span id="wpd_command_capabilities_get_supported_commands"></span>WPD\_コマンド\_機能\_取得\_サポートされている\_コマンド


ドライバーの呼び出し、 **WpdObjectCapabilities::OnGetSupportedCommands** WPD への応答ハンドラー\_コマンド\_機能\_取得\_サポートされている\_コマンドのコマンド。 ハンドラーは、さらに、サポートされているコマンドの識別子の配列を返します。

先頭に表示されるサポートされているコマンドの配列を更新する必要がありましたが、場合によっては、ハンドラーを変更する必要がない、 *WpdCapabilities.cpp*ファイル。 このような変更は、センサー デバイスも、ドライバーは、リソースをサポートするために、コマンドのオブジェクト リソース カテゴリを削除する含まれます。

```cpp
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

    // WPD_CATEGORY_CAPABILITIES
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS,
    WPD_COMMAND_CAPABILITIES_GET_COMMAND_OPTIONS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES,
    WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_EVENTS,  
    WPD_COMMAND_CAPABILITIES_GET_EVENT_OPTIONS,
};
```

## <a name="span-idwpdcommandcapabilitiesgetsupportedfunctionalcategoriesspanspan-idwpdcommandcapabilitiesgetsupportedfunctionalcategoriesspanwpdcommandcapabilitiesgetsupportedfunctionalcategories"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES"></span><span id="wpd_command_capabilities_get_supported_functional_categories"></span>WPD\_コマンド\_機能\_取得\_サポートされている\_機能\_カテゴリ


ドライバーの呼び出し、 **WpdObjectCapabilities::OnGetFunctionalCategories** WPD への応答ハンドラー\_コマンド\_機能\_取得\_サポートされている\_機能\_カテゴリ コマンド。 ハンドラーは、さらに、サポートされているカテゴリの識別子の配列を返します。

先頭に表示されるサポートされているカテゴリの配列を更新する必要がありましたが、場合によっては、ハンドラーを変更する必要がない、 *WpdCapabilities.cpp*ファイル。 これらの変更には、記憶域カテゴリを削除して、センサーのカテゴリに置き換えることが含まれます。

```cpp
const GUID g_SupportedFunctionalCategories[] =
{
    WPD_FUNCTIONAL_CATEGORY_DEVICE,
    FUNCTIONAL_CATEGORY_SENSOR_SAMPLE, // Our sensor's functional category  
};
```

ドライバーのサンプルには、カスタム機能のカテゴリの GUID が定義されています (機能\_カテゴリ\_センサー\_サンプル) センサー機能オブジェクトを記述します。

## <a name="span-idwpdcommandcapabilitiesgetfunctionalobjectsspanspan-idwpdcommandcapabilitiesgetfunctionalobjectsspanwpdcommandcapabilitiesgetfunctionalobjects"></a><span id="WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS"></span><span id="wpd_command_capabilities_get_functional_objects"></span>WPD\_コマンド\_機能\_取得\_機能\_オブジェクト


ドライバーの呼び出し、 **WpdObjectCapabilities::OnGetFunctionalObjects** WPD への応答ハンドラー\_コマンド\_機能\_取得\_機能\_オブジェクトのコマンド。 ハンドラーは、さらに、サポートされている機能のオブジェクトの識別子の配列を返します。

変更を加えて、 **OnGetFunctionalObjects** WpdBasicHardwareDriver に含まれていない、ストレージ オブジェクトのサポートを削除すると、センサー オブジェクトのサポートを追加するハンドラー。

```cpp
HRESULT WpdCapabilities::OnGetFunctionalObjects(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr                     = S_OK;
    GUID    guidFunctionalCategory = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pFunctionalObjects;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the functional category whose functional object identifiers have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY, &guidFunctionalCategory);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY");
    }

    // CoCreate a collection to store the supported functional object identifiers.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pFunctionalObjects);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported functional object identifiers for the specified functional
    // category to the collection.
    if (hr == S_OK)
    {
        PROPVARIANT pv = {0};
        PropVariantInit(&pv);
        // Don't call PropVariantClear, since we did not allocate the memory for these object identifiers

        // Add WPD_DEVICE_OBJECT_ID to the functional object identifiers collection
        if (hr == S_OK)
        {
           
            if ((guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_DEVICE) ||
                (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
            {
                pv.vt       = VT_LPWSTR;
                pv.pwszVal  = WPD_DEVICE_OBJECT_ID;
                hr = pFunctionalObjects->Add(&pv);
                CHECK_HR(hr, "Failed to add device object ID");
            }
        }

        // Add FUNCTIONAL_CATEGORY_SENSOR_SAMPLE to the functional object 
        // identifiers collection
        if (hr == S_OK)
        {
            if ((guidFunctionalCategory  == FUNCTIONAL_CATEGORY_SENSOR_SAMPLE) ||
                (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
            {
                pv.vt       = VT_LPWSTR;
                pv.pwszVal  = SENSOR_OBJECT_ID;
                hr = pFunctionalObjects->Add(&pv);
                CHECK_HR(hr, "Failed to add sensor object ID");
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS, pFunctionalObjects);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS");
    }

    return hr;
}
```

## <a name="span-idwpdcommandcapabilitiesgetsupportedcontenttypesspanspan-idwpdcommandcapabilitiesgetsupportedcontenttypesspanwpdcommandcapabilitiesgetsupportedcontenttypes"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_CONTENT_TYPES"></span><span id="wpd_command_capabilities_get_supported_content_types"></span>WPD\_コマンド\_機能\_取得\_サポートされている\_コンテンツ\_型


ドライバーの呼び出し、 **WpdObjectCapabilities::OnGetSupportedContentTypes** WPD への応答ハンドラー\_コマンド\_機能\_取得\_サポートされている\_コンテンツ\_型コマンド。 センサー デバイスはあらゆるコンテンツ タイプをサポートしないために、このハンドラーは、空のコレクションを返します。

変更を加えて、 **OnGetSupportedContentTypes**ハンドラーに含まれる、返されたコレクションにドキュメントとフォルダーのコンテンツ タイプを追加した WpdHelloWorldSample ドライバーのコードを削除します。

```cpp
HRESULT WpdCapabilities::OnGetSupportedContentTypes(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr                     = S_OK;
    GUID    guidFunctionalCategory = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pContentTypes;

    // First get ALL parameters for this command. If we cannot get ALL parameters
    // then E_INVALIDARG should be returned 
    // and no further processing should occur.

    // Get the functional category whose supported content types 
    // have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY, 
                                   &guidFunctionalCategory);
        CHECK_HR(hr, 
                 "Missing value for 
                  WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY");
    }

    // CoCreate a collection to store the supported content types.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pContentTypes);
        CHECK_HR(hr, 
                 "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Set the WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES, 
                                        pContentTypes);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES");
    }

    return hr;
}
```

## <a name="span-idwpdcommandcapabilitiesgetsupportedformatsspanspan-idwpdcommandcapabilitiesgetsupportedformatsspanwpdcommandcapabilitiesgetsupportedformats"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMATS"></span><span id="wpd_command_capabilities_get_supported_formats"></span>WPD\_コマンド\_機能\_取得\_サポートされている\_書式設定


ドライバーの呼び出し、 **WpdObjectCapabilities::OnGetSupportedFormats** WPD への応答ハンドラー\_コマンド\_機能\_取得\_サポートされている\_形式のコマンド。 センサー デバイスはあらゆるコンテンツ タイプをサポートしないためにはありません形式がサポートされているか。 その結果、このハンドラーは、空のコレクションも返します。

変更を加えて、 **OnGetSupportedContentTypes**ハンドラーは、テキスト形式をコレクションに追加した WpdHelloWorldSample ドライバーのコードを削除する必要があります。 ドキュメントのコンテンツの種類のテキスト形式がサポートされます。

```cpp
HRESULT WpdCapabilities::OnGetSupportedFormats(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr              = S_OK;
    GUID    guidContentType = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pFormats;

    // First get ALL parameters for this command. If we cannot get ALL parameters
    // then E_INVALIDARG should be returned 
    // and no further processing should occur.

    // Get the content type whose supported formats have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_CONTENT_TYPE, 
                                   &guidContentType);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_CONTENT_TYPE");
    }

    // CoCreate a collection to store the supported formats.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pFormats);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Set the WPD_PROPERTY_CAPABILITIES_FORMATS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_FORMATS, 
                                        pFormats);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_FORMATS");
    }

    return hr;
}
```

## <a name="span-idwpdcommandcapabilitiesgetsupportedeventsspanspan-idwpdcommandcapabilitiesgetsupportedeventsspanwpdcommandcapabilitiesgetsupportedevents"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_EVENTS"></span><span id="wpd_command_capabilities_get_supported_events"></span>WPD\_コマンド\_機能\_取得\_サポートされている\_イベント


ドライバーの呼び出し、 **WpdObjectCapabilities::OnGetSupportedEvents** WPD への応答ハンドラー\_コマンド\_機能\_取得\_サポートされている\_イベント コマンド。 センサー デバイス カスタム イベントのセンサー読み取り更新されたため、(イベント\_センサー\_読み取り\_更新)、ソース ファイルを更新する必要がありました。

G を追加する最初の変更が関係する\_を 1 つのサポートされているイベントの識別子を含む SupportedEvents 配列。

```cpp
const GUID g_SupportedEvents[] =
{
    EVENT_SENSOR_READING_UPDATED,
};
```

2 番目の変更を**OnGetSupportedEvents**ハンドラー、関係がサポートされているイベントのコレクションを設定するコードを追加します。

```cpp
HRESULT WpdCapabilities::OnGetSupportedEvents(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDevicePropVariantCollection> pEvents;
    UNREFERENCED_PARAMETER(pParams);

    // CoCreate a collection to store the supported events.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pEvents);
        CHECK_HR(hr, 
                 "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported events to the collection.
    if (hr == S_OK)
    {
        // populate the supported events collection
        for (DWORD dwIndex = 0; dwIndex < ARRAYSIZE(g_SupportedEvents); dwIndex++)
        {
            PROPVARIANT pv = {0};
            PropVariantInit(&pv);
            // Don't call PropVariantClear, 
            // since we did not allocate the memory for these GUIDs

            pv.vt    = VT_CLSID;
            pv.puuid = (GUID*) &g_SupportedEvents[dwIndex];

            hr = pEvents->Add(&pv);
            CHECK_HR(hr, "Failed to add supported event at index %d", dwIndex);
            if (FAILED(hr))
            {
                break;
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_SUPPORTED_EVENTS value in the results.
    if (hr == S_OK)
    {
        hr = pResults-> 
             SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_SUPPORTED_EVENTS, 
                              pEvents);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_SUPPORTED_EVENTS");
    }

    return hr;
}
```

## <a name="span-idwpdcommandcapabilitiesgeteventoptionsspanspan-idwpdcommandcapabilitiesgeteventoptionsspanwpdcommandcapabilitiesgeteventoptions"></a><span id="WPD_COMMAND_CAPABILITIES_GET_EVENT_OPTIONS"></span><span id="wpd_command_capabilities_get_event_options"></span>WPD\_コマンド\_機能\_取得\_イベント\_オプション


ドライバーの呼び出し、 **WpdObjectCapabilities::OnGetEventOptions** WPD への応答ハンドラー\_コマンド\_機能\_取得\_イベント\_オプションコマンド。 このオプションであることを示すフラグを追加する必要がありましたセンサー デバイスはブロードキャスト イベントで、更新された読み取りイベントをサポートするため (WPD\_イベント\_オプション\_IS\_ブロードキャスト\_イベント) は**TRUE**:

```cpp
HRESULT WpdCapabilities::OnGetEventOptions(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr    = S_OK;
    GUID    Event = GUID_NULL;
    CComPtr<IPortableDeviceValues> pOptions;

    // First get ALL parameters for this command. If we cannot get ALL parameters
    // then E_INVALIDARG should be returned 
    // and no further processing should occur.

    // Get the event whose options have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_EVENT, &Event);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_EVENT");
    }

    // CoCreate a collection to store the event options.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pOptions);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValues");
    }

    // Add event options to the collection
    if (hr == S_OK)
    {
        //  Check for the events we support
        if (Event == EVENT_ SENSOR_READING_UPDATED)
        {
            // These events are broadcast events
            hr = pOptions->SetBoolValue(WPD_EVENT_OPTION_IS_BROADCAST_EVENT, 
                                        TRUE);
            CHECK_HR(hr, "Failed to set WPD_EVENT_OPTION_IS_BROADCAST_EVENT");
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_EVENT_OPTIONS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_EVENT_OPTIONS, 
                                        pOptions);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_EVENT_OPTIONS");
    }

    return hr;
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 






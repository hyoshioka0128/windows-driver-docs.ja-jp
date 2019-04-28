---
Description: レンダリング プロファイルのサポート
title: レンダリング プロファイルのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f63bf4649bc0e378f0784a6e4a51c63f13c0b47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380844"
---
# <a name="supporting-rendering-profiles"></a>レンダリング プロファイルのサポート


オーディオまたはビデオ デバイスは特定のレンダリングのプロファイルに対応します。 たとえば、ストリーミング オーディオ デバイスでは、複数のチャネル特定の種類の特定のビットレートでコンテンツをストリームする可能性があります。 コンテンツの種類、ストリーミングのビットレートとチャネルの数と呼びます、*レンダリング プロファイル*します。

WPD アプリケーションは、ドライバーから多くの場合、レンダリングのプロファイルを取得します。 アプリケーションがレンダリング プロファイルを取得する方法の詳細については、次を参照してください。、[デバイスでサポートされるレンダリング機能を取得する](https://go.microsoft.com/fwlink/p/?linkid=150363)WPD SDK のトピックです。

このトピックでは、WpdWudfSampleDriver ドライバーがオーディオのストリーミング サポートを実装する方法について説明します、 *Helpers.cpp*モジュール。

ドライバーが、WPD を受信するアプリケーションでは、レンダリングのプロファイルを要求、\_コマンド\_オブジェクト\_プロパティ\_GET コマンドの WPD コマンド カテゴリで\_カテゴリ\_オブジェクト\_プロパティと、WPD\_プロパティ\_オブジェクト\_プロパティ\_オブジェクト\_RenderingInformation の ID。 このコマンドの受信が SetRenderingProfile 関数の呼び出しをトリガーする、サンプル ドライバー、 *Helpers.cpp*モジュール。

```ManagedCPlusPlus
HRESULT SetRenderingProfiles(
    IPortableDeviceValues*          pValues)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDeviceValues> pPreferredProfile;
    CComPtr<IPortableDeviceValues> pProfile2;

    CComPtr<IPortableDeviceValuesCollection> pProfiles;

    if(pValues == NULL)
    {
        hr = E_POINTER;
        CHECK_HR(hr, ("Cannot have NULL parameter"));
        return hr;
    }

    // Create the collection to hold the profiles
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValuesCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValuesCollection,
                              (VOID**) &pProfiles);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValuesCollection");
    }

    // Get the preferred audio profile
    if (hr == S_OK)
    {
        hr = GetPreferredAudioProfile(&pPreferredProfile);
        CHECK_HR(hr, "Failed to get preferred audio profile properties");
    }

    // Add the profile
    if (hr == S_OK)
    {
        hr = pProfiles->Add(pPreferredProfile);
        CHECK_HR(hr, "Failed to add preferred audio profile to profile collection");
    }

    // Get the second audio profile
    if (hr == S_OK)
    {
        hr = GetAudioProfile2(&pProfile2);
        CHECK_HR(hr, "Failed to get second audio profile properties");
    }

    // Add the profile
    if (hr == S_OK)
    {
        hr = pProfiles->Add(pProfile2);
        CHECK_HR(hr, "Failed to add second audio profile to profile collection");
    }

    // Set the WPD_RENDERING_INFORMATION_PROFILES
    if (hr == S_OK)
    {
        hr = pValues->SetIPortableDeviceValuesCollectionValue(WPD_RENDERING_INFORMATION_PROFILES, pProfiles);
        CHECK_HR(hr, "Failed to set WPD_RENDERING_INFORMATION_PROFILES");
    }

    return hr;
}
```

**SetRenderingProfiles**関数、さらに、IPortableDeviceValues オブジェクトの実際のプロファイル情報を返します、GetPreferredAudioProfile ヘルパー関数を呼び出します。

```ManagedCPlusPlus
HRESULT GetPreferredAudioProfile(
    IPortableDeviceValues** ppProfile)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDeviceValues> pProfile;

    if(ppProfile == NULL)
    {
        hr = E_POINTER;
        CHECK_HR(hr, ("Cannot have NULL parameter"));
        return hr;
    }

    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pProfile);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValues");
    }

    // Set the value for WPD_OBJECT_FORMAT to indicate this profile applies to WMA objects
    if (hr == S_OK)
    {
        hr = pProfile->SetGuidValue(WPD_OBJECT_FORMAT, WPD_OBJECT_FORMAT_WMA);
        CHECK_HR(hr, "Failed to set WPD_OBJECT_FORMAT");
    }

    // Set the preferred value for WPD_MEDIA_TOTAL_BITRATE
    if (hr == S_OK)
    {
        hr = pProfile->SetUnsignedIntegerValue(WPD_MEDIA_TOTAL_BITRATE, 192000);
        CHECK_HR(hr, "Failed to set WPD_MEDIA_TOTAL_BITRATE");
    }

    // Set the preferred value for WPD_AUDIO_CHANNEL_COUNT
    if (hr == S_OK)
    {
        hr = pProfile->SetUnsignedIntegerValue(WPD_AUDIO_CHANNEL_COUNT, 2);
        CHECK_HR(hr, "Failed to set WPD_AUDIO_CHANNEL_COUNT");
    }

    // Set the preferred value for WPD_AUDIO_FORMAT_CODE
    if (hr == S_OK)
    {
        hr = pProfile->SetUnsignedIntegerValue(WPD_AUDIO_FORMAT_CODE, WAVE_FORMAT_MSAUDIO3);
        CHECK_HR(hr, "Failed to set WPD_AUDIO_FORMAT_CODE");
    }

    // Set the output result
    if (hr == S_OK)
    {
        hr = pProfile->QueryInterface(IID_PPV_ARGS(ppProfile));
        CHECK_HR(hr, "Failed to QI for IPortableDeviceValues");
    }

    return hr;
}
```

 

 





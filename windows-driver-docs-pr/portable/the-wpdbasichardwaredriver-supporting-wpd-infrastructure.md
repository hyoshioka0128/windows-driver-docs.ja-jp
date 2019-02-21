---
Description: Support for WPD infrastructure (WpdBasicHardwareDriverSample)
title: WPD インフラストラクチャ (WpdBasicHardwareDriverSample) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4716963f8530b5b4adc7865996c81387010c1392
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548679"
---
# <a name="support-for-wpd-infrastructure-wpdbasichardwaredriversample"></a>WPD インフラストラクチャ (WpdBasicHardwareDriverSample) のサポート


WPD インフラストラクチャは、コマンドの駆動型です。 WPD アプリケーションを呼び出すと、メソッドのいずれかの特定のインターフェイスで、WPD シリアライザー (インプロセス COM サーバー)、ドライバーに送信する 1 つまたは複数のコマンドに、メソッドの呼び出しに変換します。 ドライバーは、これらのコマンドを処理し、応答を返します。 インフラストラクチャの詳細については、次を参照してください。、[アーキテクチャの概要](architecture-overview.md)トピック。

次の図の*WpdMon.exe*ツールは、アプリケーション呼び出しの結果を表示、 **IPortableDeviceProperties::GetPropertyAttributes**のプロパティを取得するメソッドの属性は、気温・湿度センサー。

![wpd モニター ](images/wpdmon_get_attributes.png)

WPD シリアライザーが変換前の画像で、 **GetPropertyAttributes** WPD 呼び出せる\_コマンド\_オブジェクト\_プロパティ\_取得\_属性コマンドと、対応するパラメーター。 ドライバーは、このコマンドを処理し、WPD API への応答を発行します。

WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_で属性コマンドが処理された最初の**WpdObjectProperties::DispatchWpdMessage**メソッド。 さらに、このメソッドを呼び出す、 **WpdObjectProperties::OnGetPropertyAttributes**メソッド。 これらのメソッドの両方にあるは、 *WpdObjectProperties.cpp*ソース ファイル。

次の抜粋、 **WpdObjectProperties::DispatchWpdMessage**メソッド*WpdObjectProperties.cpp*への呼び出しを示しています、 **WpdObjectProperties::OnGetPropertyAttributes**ハンドラーのプロパティの属性を取得します。 **DispatchWpdMessage**メソッドは、ハンドラーをコマンド パラメーターを渡します。 これらのパラメーターには、ドライバーを取得するプロパティを持つオブジェクトのオブジェクト識別子が含まれます。 さらに、パラメーターには取得する属性を識別するプロパティのキーのコレクションが含まれます。

```cpp
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
            CHECK_HR(hr, 
                     "This object does not support this command category %ws",
                     CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
     …
        else if(IsEqualPropertyKey(Command, 
                                   WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES))
        {
            hr = OnGetPropertyAttributes(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get property attributes");
            }
        }
        …
    return hr;
}
```

**WpdObjectProperties::OnGetPropertyAttributes**メソッドは、デバイスの値 (IPortableDeviceValues) のコレクションで要求された属性のコレクションを返します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 






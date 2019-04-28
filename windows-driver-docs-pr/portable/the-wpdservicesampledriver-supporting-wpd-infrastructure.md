---
Description: WPD インフラストラクチャ (WpdServiceSampleDriverSample) のサポート
title: WPD インフラストラクチャ (WpdServiceSampleDriverSample) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe81c865bfd908cef9689ba1d910b801508eb81d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370483"
---
# <a name="support-for-wpd-infrastructure-wpdservicesampledriversample"></a>WPD インフラストラクチャ (WpdServiceSampleDriverSample) のサポート


WPD インフラストラクチャは、コマンドの駆動型です。 WPD アプリケーションを呼び出すと、メソッドのいずれかの特定のインターフェイスで、WPD シリアライザー (インプロセス COM サーバー)、ドライバーに送信する 1 つまたは複数のコマンドに、メソッドの呼び出しに変換します。 さらに、ドライバーは、これらのコマンドを処理し、応答を返します。 インフラストラクチャの詳細については、次を参照してください。、[アーキテクチャの概要](architecture-overview.md)トピック。

次の図の*WpdMon.exe*ツールは、アプリケーション呼び出しの結果を表示、 **IPortableDeviceServiceMethods::Invoke**でサポートされている BeginSync メソッドを呼び出すメソッドをドライバーのサンプル:

![wpd モニター](images/iportabledeviceservicemethods_invoke_method_wpdmon.png)

WPD シリアライザーが変換前の画像で、 **Invoke** WPD 呼び出せる\_コマンド\_サービス\_メソッド\_開始\_INVOKE コマンド、対応するパラメーターです。 ドライバーは、このコマンドを処理し、WPD API への 2 つの応答を発行します。 最初の応答は、結果の WPD\_コマンド\_サービス\_メソッド\_開始\_ことを示すために INVOKE を**StartInvoke**コマンドが成功したこととメソッドは、デバイス上で実行を開始します。 2 番目の応答は、WPD\_イベント\_サービス\_メソッド\_メソッドの完了時に、ドライバーが送信完了イベント。 ドライバーに送信される WPD\_イベント\_サービス\_メソッド\_を完了することで、WPD API は、必要なメソッドの完了とクリーンアップを実行可能性があります。 サンプル ドライバーでは、2 つの応答の直後に時間遅延なく;実際のデバイスで遅延が発生でく、2 つの応答の間でメソッドを完了する時間がかかる場合。

WPD\_コマンド\_サービス\_メソッド\_開始\_で INVOKE コマンドが処理された最初の**WpdService::DispatchWpdMessage**メソッド。 さらに、このメソッドを呼び出す、 **WpdServiceMethod::OnStartInvoke**メソッド。 最初のメソッドは、ファイルで見つかった*WpdService.cpp*; 2 つ目は、ファイルで見つかった*WpdServiceMethod.cpp*。

次の抜粋、 **WpdService::DispatchWpdMessage**メソッド*WpdService.cpp*への呼び出しを示しています、 **WpdServiceMethod::OnStartInvoke**ハンドラー。 **DispatchWpdMessage**メソッドは、ハンドラーをコマンド パラメーターを渡します。 これらのコマンド パラメーターのパラメーターへのポインターから成る、 **Invoke**メソッドとへのポインター、 *pResults*メソッドの結果を受け取る変数。

```cpp
HRESULT WpdService::DispatchWpdMessage(
            REFPROPERTYKEY         Command,
    __in    IPortableDeviceValues* pParams,
    __out   IPortableDeviceValues* pResults)
{
    HRESULT     hr                  = S_OK;
    LPWSTR      pszRequestFilename  = NULL;

    // Get the request filename to process the service message
    hr = pParams->GetStringValue(PRIVATE_SAMPLE_DRIVER_REQUEST_FILENAME, &pszRequestFilename);
    if (FAILED(hr))
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Failed to get the required requested filename");
    }

    if (hr == S_OK)
    {    
        hr = CheckRequestFilename(pszRequestFilename);
        CHECK_HR(hr, "Unknown request filename %ws received", pszRequestFilename);
    }

    if (hr == S_OK)
    {
     …
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_SERVICE_METHODS_START_INVOKE))
        {
            hr = m_ServiceMethods.OnStartInvoke(pParams, pResults);
        }
        …
    return hr;
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdServiceSampleDriverSample](the-wpdservicesampledriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 






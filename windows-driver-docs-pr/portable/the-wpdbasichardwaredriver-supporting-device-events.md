---
Description: Supporting Device Events
title: デバイスのイベントをサポートしています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 635a977b619c5783b9f60d3f0787e8ad114bf465
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552296"
---
# <a name="supporting-device-events"></a>デバイスのイベントをサポートしています。


ドライバーのサンプルを定義し、WPD センサー機能のオブジェクトに関連付けられているカスタム WPD イベントをサポートする\_イベント\_センサー\_読み取り\_更新されました。

このカスタム イベントは、新しいセンサー読み取りが利用できることをすべて接続されているクライアントに通知に送信されます。 次の表では、パラメーターについて説明します。

| パラメーター名                   | 説明                                                         |
|----------------------------------|---------------------------------------------------------------------|
| WPD\_イベント\_パラメーター\_イベント\_ID | WPD に GUID 値が設定\_イベント\_センサー\_読み取り\_更新されました。          |
| センサー\_読み取り                  | センサーの読み取りを含む符号なしの大きな整数値を指定します。   |
| センサー\_UPDATE\_間隔         | センサーの更新間隔を含む符号なし整数値を指定します。 |



このカスタム イベントのイベントの GUID が定義されている*Stdafx.h*します。 **WpdBaseDriver::ProcessReadData**、ドライバー呼び出し**WpdBaseDriver::PostSensorReadingEvent**センサーの読み取りを抽出して後から読み取り要求の場合は、間隔を更新しを変換DWORD 値です。

**WpdBaseDriver::PostSensorReadingEvent**次の手順を完了します。

1.  初期化します、 **IPortableDeviceValues**イベント パラメーターを保持します。
2.  シリアル化、 **IPortableDeviceValues**バイト バッファーにします。
3.  呼び出し**IWDFDevice::PostEvent** WPD に EventGuid 設定を持つ\_イベント\_通知、イベントの種類のセットを WdfEventBroadcast、およびイベントのパラメーターのシリアル化されたバイト バッファー。

```cpp
if (hr == S_OK)
{
    // Initialize the event parameters
    m_pEventParams->Clear();

    // Populate the event parameters
    hr = m_pEventParams-> 
         SetGuidValue(WPD_EVENT_PARAMETER_EVENT_ID, 
                      WPD_EVENT_SENSOR_READING_UPDATED);
    CHECK_HR(hr, "Failed to set the WPD_EVENT_PARAMETER_EVENT_ID");
}

if (hr == S_OK)
{
    hr = m_pEventParams->SetUnsignedLargeIntegerValue(SENSOR_READING, 
                                                 llSensorData);
    CHECK_HR(hr, "Failed to set the sensor reading");
}

if (hr == S_OK)
{
    hr = m_pEventParams->SetUnsignedIntegerValue(SENSOR_UPDATE_INTERVAL, dwUpdateInterval);
    CHECK_HR(hr, "Failed to set the sensor update interval");
}

if (hr == S_OK)
{
    // Create a buffer with the serialized parameters
    hr = m_pWpdSerializer->GetBufferFromIPortableDeviceValues(m_pEventParams,  
                                                              &pBuffer,
                                                              &cbBuffer);
    CHECK_HR(hr, "Failed to get buffer from IPortableDeviceValues");
}
// Send the event
if (hr == S_OK)
{
    hr = m_pWDFDevice->PostEvent(WPD_EVENT_NOTIFICATION, 
                                 WdfEventBroadcast, 
                                 pBuffer, 
                                 cbBuffer);
    CHECK_HR(hr, "Failed to post the WPD broadcast event");
}
```

WPD イベントを受信するには、アプリケーションで実装、 **IPortableDeviceEventCallback::OnEvent**コールバック メソッドを呼び出します**IPortableDevice::Advise**イベントを受信するように登録するには通知のコールバック。

イベントのコールバック、アプリケーションがチェックするイベントの GUID が WPD と一致するかどうか\_イベント\_センサー\_読み取り\_更新とイベントのパラメーターからのセンサーの読み取りと間隔のデータを取得します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)










---
Description: Support for property commands (WpdBasicHardwareDriverSample)
title: プロパティ コマンド (WpdBasicHardwareDriverSample) のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a315c469505b22171807de43c11a69f63a84b873
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528364"
---
# <a name="supporting-wpd-property-commands-wpdbasichardwaredriversample"></a>WPD プロパティ コマンド (WpdBasicHardwareDriverSample) をサポート


ドライバーのサンプルでは、6 つのプロパティのコマンドをサポートします。 これらのコマンドが最初に、処理、 **WpdObjectProperties::DispatchMessage**メソッドを対応するコマンド ハンドラーが呼び出されます。 **DispatchMessage**メソッドと個別のハンドラーは、すべてで、 *WpdObjectProperties.cpp*ファイル。

次の表の情報は、説明の各プロパティがサポートされているコマンドのハンドラーの名前と共にを**WpdObjectProperties::DispatchMessage**特定のコマンドを処理するときに呼び出します。

| コマンド                                           | ハンドラー                  | 説明                                                                                          |
|---------------------------------------------------|--------------------------|------------------------------------------------------------------------------------------------------|
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_サポートされています。  | OnGetSupportedProperties | 指定したオブジェクトのプロパティのキーの配列を返します。                                              |
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得             | OnGetPropertyValues      | ドライバーに渡されるプロパティのキーに対応するプロパティ値のコレクションを返します。 |
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_すべて        | OnGetAllProperties       | 指定したオブジェクトのすべてのプロパティ値を返します。                                                  |
| WPD\_コマンド\_オブジェクト\_プロパティ\_設定             | OnSetPropertyValues      | デバイスでは、指定されたプロパティ値を設定します。                                                     |
| WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_属性 | OnGetPropertyAttributes  | 指定したオブジェクトでは、1 つまたは複数のプロパティの属性のコレクションを返します。                     |
| WPD\_コマンド\_オブジェクト\_プロパティ\_削除          | OnDeleteProperties       | 指定したプロパティのキーによって識別されるプロパティを削除します。                               |



## <a name="span-idwpdcommandobjectpropertiesgetsupportedspanspan-idwpdcommandobjectpropertiesgetsupportedspanwpdcommandobjectpropertiesgetsupported"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_SUPPORTED"></span><span id="wpd_command_object_properties_get_supported"></span>WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_サポートされています。


ドライバーの呼び出し、 **WpdObjectProperties::OnGetSupportedProperties** WPD への応答ハンドラー\_コマンド\_オブジェクト\_プロパティ\_取得\_サポートされているコマンド。 ハンドラーが呼び出されます、 **AddSupportedPropertyKeys**要求されたオブジェクトのサポートされているキーを取得します。

サンプル デバイスが WpdHelloWorldSample ドライバーで記憶域、フォルダー、またはファイル オブジェクトをサポートしていませんし、新しいドライバーには、元のドライバーに含まれていないオブジェクトがサポートされているため、更新、 **AddSupportedPropertyKeys**メソッドが必要でした。

次のコードの実行から、変更された**AddSupportedPropertyKeys**メソッド。 このメソッドは 2 つのサポート メソッドを呼び出します (**AddDevicePropertyKeys**と**AddSensorPropertyKeys**)、要求されたオブジェクトのキーを取得します。

```cpp
HRESULT AddSupportedPropertyKeys(
    LPCWSTR                        wszObjectID,
    IPortableDeviceKeyCollection*  pKeys)
{
    HRESULT     hr          = S_OK;
    CAtlStringW strObjectID = wszObjectID;

    // Add Common PROPERTYKEYs for ALL WPD objects
    AddCommonPropertyKeys(pKeys);

    if (strObjectID.CompareNoCase(WPD_DEVICE_OBJECT_ID) == 0)
    {
        // Add the PROPERTYKEYs for the &#39;DEVICE&#39; object
        AddDevicePropertyKeys(pKeys);
    }

    // Add other PROPERTYKEYs for other supported objects...
    if (
           (strObjectID.CompareNoCase(SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(TEMP_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(FLEX_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(PIR_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(PING_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(QTI_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(MEMSIC_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(HITACHI_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(PIEZO_SENSOR_OBJECT_ID) == 0) ||
           (strObjectID.CompareNoCase(COMPASS_SENSOR_OBJECT_ID) == 0)
       )
    {
        // Add the PROPERTYKEYs for the Sensor object
        AddSensorPropertyKeys(pKeys);
    }

    return hr;
}
```

## <a name="span-idwpdcommandobjectpropertiesgetspanspan-idwpdcommandobjectpropertiesgetspanwpdcommandobjectpropertiesget"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET"></span><span id="wpd_command_object_properties_get"></span>WPD\_コマンド\_オブジェクト\_プロパティ\_取得


ドライバーの呼び出し、 **WpdObjectProperties::OnGetPropertyValues** WPD への応答ハンドラー\_コマンド\_オブジェクト\_プロパティ\_GET コマンド。 ハンドラーがさらに、呼び出し、 **GetPropertyValuesForObject**要求されたプロパティの現在の値を取得します。 センサー デバイスは、WpdHelloWorldSample ドライバーで検出された記憶域、フォルダー、またはファイル オブジェクトをサポートしていないため、新しいドライバーには、元のドライバーで見つからなかったオブジェクトがサポートされているため、このメソッドの更新が必要でした。

デバイス オブジェクトのプロパティが返されるコードがそのままは残っています。 これは、ファームウェアのバージョン、電力レベル、電源、デバイスのプロトコル、デバイス モデル、およびに返されるコードです。

このコードは変更されませんでしたが WpdHelloWorldSample ドライバーによって返されたプロパティ値からサンプル ドライバーによって返されたデバイス モデル (およびその他の同様のプロパティ) が異なります。 これは、内の定義を更新したため*WpdObjectProperties.h*:

```cpp
#define DEVICE_PROTOCOL_VALUE                L"Sensor Protocol ver 1.00"
#define DEVICE_FIRMWARE_VERSION_VALUE        L"1.0.0.0"
#define DEVICE_POWER_LEVEL_VALUE             100
#define DEVICE_MODEL_VALUE                   L"RS232 Sensor"
#define DEVICE_FRIENDLY_NAME_VALUE           L"Parallax BS2 Sensor"
#define DEVICE_MANUFACTURER_VALUE            L"Windows Portable Devices Group"
#define DEVICE_SERIAL_NUMBER_VALUE           L"01234567890123-45676890123456"
#define DEVICE_SUPPORTS_NONCONSUMABLE_VALUE  FALSE
```

次の表で定義*WpdObjectProperties.h*、WpdHelloWorldSample から元の値とドライバーのサンプルで指定されている新しい値。

| 定義                             | 元の値              | 新しい値                   |
|----------------------------------------|-----------------------------|-----------------------------|
| デバイス\_プロトコル\_値                | Hello World v1.00 のプロトコル  | センサー プロトコル v1.00       |
| デバイス\_ファームウェア\_バージョン              | 1.0.0.0                     | 1.0.0.0                     |
| デバイス\_POWER\_レベル                   | 100                         | 100                         |
| デバイス\_モデル\_値                   | ハローワールド！                | Rs-232 センサー               |
| デバイス\_フレンドリ\_名                 | ハローワールド！                | 視差 BS2 センサー         |
| デバイス\_製造元\_値            | WPD グループ                   | WPD グループ                   |
| デバイス\_シリアル\_数\_値          | 012345678901234567890123456 | 012345678901234567890123456 |
| デバイス\_サポート\_NONCONSUMABLE\_値 | **FALSE**                   | **FALSE**                   |



最も大きな変更点、 **GetPropertyValuesForObject**センサー プロパティを取得するセクションではメソッドが発生しました。 このコードで定義されているいくつかの値を取得する*WpdObjectProperties.h*オブジェクト名、その形式、そのコンテンツの種類など、削除するかどうか。

さらに、このコードは、現在のセンサー読み取り値とセンサー更新間隔も取得します。 これらの最後の 2 つのプロパティは、2 つのヘルパー関数を呼び出すことによって取得されます。**GetSensorReading**と**GetUpdateInterval**します。

次の抜粋、 **GetPropertyValuesForObject**メソッドには、センサー オブジェクトのプロパティを取得するコードが含まれています。

```cpp
// Retrieve the sensor properties

        else if (
                    (strObjectID.CompareNoCase(SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(TEMP_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(FLEX_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(PIR_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(PING_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(QTI_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(MEMSIC_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(HITACHI_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(PIEZO_SENSOR_OBJECT_ID) == 0) ||
                    (strObjectID.CompareNoCase(COMPASS_SENSOR_OBJECT_ID) == 0)
                 )
        {
            for (DWORD dwIndex = 0; dwIndex < cKeys; dwIndex++)
            {
                PROPERTYKEY Key = WPD_PROPERTY_NULL;
                hr = pKeys->GetAt(dwIndex, &Key);
                CHECK_HR(hr, "Failed to get PROPERTYKEY at index %d in collection", dwIndex);

                if (hr == S_OK)
                {
                    // Preset the property value to &#39;error not supported&#39;.  The actual value
                    // will replace this value, if read from the device.
                    pValues->SetErrorValue(Key, HRESULT_FROM_WIN32(ERROR_NOT_SUPPORTED));
                    if (IsEqualPropertyKey(Key, WPD_OBJECT_ID))
                    {
                        hr = pValues->SetStringValue(WPD_OBJECT_ID, strObjectID);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_ID");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_PERSISTENT_UNIQUE_ID))
                    {

                        // Retrieve the ID of the sensor using the m_SensorType member of the
                        // basedriver that is set during the data-read operation.
                        hr = pValues->SetStringValue(WPD_OBJECT_PERSISTENT_UNIQUE_ID, strObjectID);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_PERSISTENT_UNIQUE_ID");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_PARENT_ID))
                    {
                        hr = pValues->SetStringValue(WPD_OBJECT_PARENT_ID, WPD_DEVICE_OBJECT_ID);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_PARENT_ID");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_NAME))
                    {
                        // Retrieve the name of the sensor using the m_SensorType member of the
                        // basedriver that is set during the data-read operation.
                        if (m_pBaseDriver->m_SensorType == 0)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 2)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, TEMP_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 3)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, FLEX_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 4)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, PING_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 5)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, PIR_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 6)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, MEMSIC_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 7)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, QTI_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 8)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, PIEZO_SENSOR_OBJECT_NAME_VALUE);
                        else if (m_pBaseDriver->m_SensorType == 9)
                            hr = pValues->SetStringValue(WPD_OBJECT_NAME, HITACHI_SENSOR_OBJECT_NAME_VALUE);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_NAME");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_FORMAT))
                    {
                        hr = pValues->SetGuidValue(WPD_OBJECT_FORMAT, WPD_OBJECT_FORMAT_UNSPECIFIED);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_FORMAT");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_CONTENT_TYPE))
                    {
                        hr = pValues->SetGuidValue(WPD_OBJECT_CONTENT_TYPE, WPD_CONTENT_TYPE_FUNCTIONAL_OBJECT);
CHECK_HR(hr, "Failed to set WPD_OBJECT_CONTENT_TYPE");
                    }

                    else if (IsEqualPropertyKey(Key, WPD_OBJECT_CAN_DELETE))
                    {
                        hr = pValues->SetBoolValue(WPD_OBJECT_CAN_DELETE, FALSE);
                        CHECK_HR(hr, "Failed to set WPD_OBJECT_CAN_DELETE");
                    }

                    else if (IsEqualPropertyKey(Key, SENSOR_READING))
                    {
                        hr = pValues->SetUnsignedLargeIntegerValue(SENSOR_READING, GetSensorReading());
                        CHECK_HR(hr, "Failed to set SENSOR_READING");
                    }

                    else if (IsEqualPropertyKey(Key, SENSOR_UPDATE_INTERVAL))
                    {
                        hr = pValues->SetUnsignedLargeIntegerValue(SENSOR_UPDATE_INTERVAL, GetUpdateInterval());
                        CHECK_HR(hr, "Failed to set SENSOR_UPDATE_INTERVAL");
                    }
                    else if (IsEqualPropertyKey(Key, WPD_FUNCTIONAL_OBJECT_CATEGORY))
                    {
                        hr = pValues->SetGuidValue(WPD_FUNCTIONAL_OBJECT_CATEGORY, FUNCTIONAL_CATEGORY_SENSOR_SAMPLE);
                        CHECK_HR(hr, "Failed to set WPD_FUNCTIONAL_OBJECT_CATEGORY");
                    }
                }
             } // end for
        } // end else if
```

**GetSensorReading**ヘルパー関数を数値 (DWORD) 形式で最新のセンサーを取得します。

```cpp
LONGLONG WpdObjectProperties::GetSensorReading()
{    
    // Ensure that this value isn&#39;t currently being accessed by another thread
    CComCritSecLock<CComAutoCriticalSection> Lock(m_SensorReadingCriticalSection);

    return m_llSensorReading;
}
```

**注**クリティカル セクションがの同時実行のアクセスを防ぐために必要な*m\_llSensorReading*メンバー変数。 非同期的に、各 RS232 読み取りが完了すると、この値が上書きされますが読み取られるたびに、センサー\_WPD アプリケーションが読み取りのプロパティを取得します。



**GetUpdateInterval**ヘルパー関数と同じ操作を実行しますにアクセスする、 *m\_dwUpdateInterval*メンバー変数と数値 (DWORD) 値である場合の形式を返します。使用可能な。

```ManagedCPlusPlus
DWORD WpdObjectProperties::GetUpdateInterval()
{    
    return m_dwUpdateInterval;
}
```

注意を*m\_dwUpdateInterval* (使用する場合、たとえば、WDF 並列ディスパッチ キューは、シーケンシャルではなく、複数のスレッドがこの値をアクセスする場合、クリティカル セクションによってメンバー変数を保護する必要がありますディスパッチ キュー、または**WpdBaseDriver::ProcessReadData**代わりの初期化中に 1 回に複数回更新間隔を設定するように変更)。 わかりやすくするため、クリティカル セクションを省略するとします。

## <a name="span-idwpdcommandobjectpropertiesgetallspanspan-idwpdcommandobjectpropertiesgetallspanwpdcommandobjectpropertiesgetall"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_ALL"></span><span id="wpd_command_object_properties_get_all"></span>WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_すべて


ドライバーの呼び出し、 **WpdObjectProperties::OnGetAllPropertyValues** WPD への応答ハンドラー\_コマンド\_オブジェクト\_プロパティ\_取得\_すべてコマンド. ハンドラーがさらに、プロパティの指定したオブジェクトのキーを呼び出してすべてを取得、 **GetPropertyValuesForObject**要求されたプロパティの現在の値を取得するヘルパー関数。

## <a name="span-idwpdcommandobjectpropertiessetspanspan-idwpdcommandobjectpropertiessetspanwpdcommandobjectpropertiesset"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_SET"></span><span id="wpd_command_object_properties_set"></span>WPD\_コマンド\_オブジェクト\_プロパティ\_設定


ドライバーの呼び出し、 **WpdObjectProperties::OnSetPropertyValues** WPD への応答ハンドラー\_コマンド\_オブジェクト\_プロパティ\_SET コマンド。 記述 (したりできる設定) サンプル ドライバーのプロパティのみがセンサー\_UPDATE\_間隔。

ハンドラーは、最初に指定されたプロパティのオブジェクト識別子を確認し、プロパティ キー自体を調べます。 センサーにオブジェクト識別子が設定されている場合\_オブジェクト\_ID とプロパティのキーはセンサー\_UPDATE\_ハンドラーの呼び出しの間隔、 **SendUpdateIntervalToDevice**ヘルパー値を更新する関数。

**SendUpdateIntervalToDevice**ヘルパー関数の有効な入力値の確認し、その値を持つ書き込み要求を書式設定、デバイスへの書き込み要求を送信して、書き込み操作を実行します。

```cpp
HRESULT WpdObjectProperties::SendUpdateIntervalToDevice(DWORD dwNewInterval)
{
    HRESULT      hr                           = S_OK;
    RS232Target* pDeviceTarget                = NULL;

    CHAR  szInterval[INTERVAL_DATA_LENGTH+1]  = {0};

    // Check the input value
    if (IsValidUpdateInterval(dwNewInterval) == FALSE)
    {
        hr = HRESULT_FROM_WIN32(ERROR_INVALID_DATA);
        CHECK_HR(hr, "Invalid update interval: %d", dwNewInterval);
    }

    // Format a write request with the input value
    if (hr == S_OK)
    {
        hr = StringCchPrintfA(szInterval, 
                              ARRAYSIZE(szInterval), "%d", dwNewInterval);
        CHECK_HR(hr, "Failed to convert the new interval to a CHAR string");
    }

    // Send the write request to the device
    if (hr == S_OK)
    {
        pDeviceTarget = m_pBaseDriver->GetRS232Target();

        if (pDeviceTarget->IsReady())
        {
            hr = pDeviceTarget->
                 SendWriteRequest((BYTE *)szInterval, sizeof(szInterval));
            CHECK_HR(hr, 
                     "Failed to send the write request to 
                      set the new temperature update interval");

            if (hr == S_OK)
            {
                TraceEvents(TRACE_LEVEL_VERBOSE, TRACE_FLAG_DRIVER, 
                            "%!FUNC! Sent new interval: %s", szInterval);
            }
        }
        else
        {
            hr = HRESULT_FROM_WIN32(ERROR_NOT_READY);
            CHECK_HR(hr, "Device is not ready to receive write requests");
        }
    }

    if (hr == S_OK)
    {
        // Update the cached value on the driver
        SetUpdateInterval(dwNewInterval);
    }

    return hr;
}
```

## <a name="span-idwpdcommandobjectpropertiesgetattributesspanspan-idwpdcommandobjectpropertiesgetattributesspanwpdcommandobjectpropertiesgetattributes"></a><span id="WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES"></span><span id="wpd_command_object_properties_get_attributes"></span>WPD\_コマンド\_オブジェクト\_プロパティ\_取得\_属性


ドライバーの呼び出し、 **WpdObjectProperties::OnGetPropertyAttributes** WPD への応答ハンドラー\_コマンド\_オブジェクト\_プロパティ\_取得\_属性コマンド。 ハンドラーがさらに、呼び出し、 **GetPropertyAttributesForObject**ヘルパー関数を指定したオブジェクトの属性を取得します。

元の WpdHelloWorldSample ドライバーでは、すべてのプロパティの属性は同一ですし、すべてのプロパティが読み取り専用します。 ただし、更新されたドライバー、センサーで\_更新\_間隔は、読み取り/書き込み、および両方のセンサー\_更新\_間隔とセンサー\_読み取りがあるフォーム WPD\_プロパティ\_属性\_フォーム\_範囲。 その結果、このヘルパー関数で小さな変更が必要です。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)










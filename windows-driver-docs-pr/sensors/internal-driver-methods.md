---
title: 内部のヘルパー メソッド
description: センサー ドライバーには、数にデータをポーリング、プロパティの設定、プロパティを取得する、デバイスの状態を更新、およびイベントをサポートしているなどのタスクを実行する内部のヘルパー メソッドがサポートしています。
ms.assetid: BF5956FE-E1B6-476A-9B6E-86B400DE0A20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02df7ba4f8621f8ee4bdf8aff85a537a5c1cb294
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345199"
---
# <a name="internal-helper-methods"></a>内部のヘルパー メソッド


センサー ドライバーには、数にデータをポーリング、プロパティの設定、プロパティを取得する、デバイスの状態を更新、およびイベントをサポートしているなどのタスクを実行する内部のヘルパー メソッドがサポートしています。

## <a name="supporting-device-state-updates-for-multi-sensor-devices"></a>複数のセンサー デバイスのデバイスの状態の更新プログラムをサポートしています。


センサー ドライバーでは、複数のセンサーを含む 1 つのデバイスのデバイスの状態を設定するメソッドをサポートしています。 擬似コードを示しますこのを使用して、 **DriverUpdateDeviceState**メソッド。

```cpp
DriverUpdateDeviceState()
{
    if ((sensor device is intelligent (e.g. HID) ||
        (sensor device is simple (e.g. SPB))
    {

        // if no client is connected to any of the sensors on this device
        // then disconnect from the device
        flagConnected = false
        for (all sensors on device)
        {
            if (clientCount > 0)
            {
                flagConnected = true
            }
        }

        if (false == flagConnected)
        {
            Disconnect from device
            deviceState = deviceStateDisconnected
        }
        else
        {
            Connect to device
            deviceState = deviceStateConnected
        }
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }
}
```

## <a name="internal-methods-for-intelligent-sensors"></a>インテリジェントなセンサーの内部メソッド


センサー ドライバー (HID) のようなインテリジェントなセンサーをサポートする場合、データのポーリング、イベントを処理、プロパティを取得、プロパティの設定、電源管理をメソッドのサポートがあります。 擬似コードに示しますを使用してこれらのタスク、 **HIDSensorPollData**、 **HIDSensorSetProperties**、および**HIDSensorGetProperties**メソッド。

```cpp
HIDSensorPollData(sensorID) // Driver issues USB/HID “GET_INPUT” command to the sensor device
{
    // the driver is making a request for polled data
    // if the sensor is in a READY state respond by sending
    // the data for this sensor asynchronously to the driver
    if (true == sensorReady)
    {
        sensorState = sensorStateReady
        sensorEvent = eventTypeDataPoll
    }
    else
    {
        Set sensorState = sensorStateNoData //or failure, or initializing, or not available as appropriate
        Set sensorEvent = eventTypeStateChange
    }

    Send async data to driver //received in driver by DDIHandleAsyncDataEvent()
}
```

```cpp
HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) //SET_FEATURE
{
    if (requestedRS == reportingStateAllEvents) //reporting state
    {
        Set effectiveRS = reportingStateAllEvents
    }
    else
    {
        Set effectiveRS = reportingStateNoEvents
    }

    if (requestedPS == powerStateFullPower) //power state
    {
        Set effectivePS = powerStateFullPower
    }
    else if (requestedPS == powerStateLowPower)
    {
        Set effectivePS = powerStateLowPower
    }
    else
    {
        Set effectivePS = powerStatePowerOff
    }

    if (can support requestedCRI)
    {
        Set effectiveCRI = requestedCRI
    }
    else
    {
        Set effectiveCRI = value that can be supported
    }

    if (can support requestedCS[])
    {
        Set effectiveCS[] = requestedCS[]
    }
    else
    {
        Set effectiveCS[] = values that can be supported
    }

    if (requestedLDA == locDesiredAccuracyHigh) //location desired accuracy
    {
        Set effectiveLDA = locDesiredAccuracyHigh
    }
    else
    {
        Set effectiveLDA = locDesiredAccuracyDefault
    }


}
```

```cpp
HIDSensorGetProperties(sensorID, RS, PS, CRI, CS[], LDA) //Driver issues USB/HID “GET_FEATURE” command to the sensor
{
    buffer.effectiveRS
    buffer.effectivePS
    buffer.effectiveCRI
    buffer.effectiveCS[]
    buffer.effectiveLDA

    // The sensor device can optionally also override the following properties
    buffer.sensorCategory
    buffer.sensorType
    buffer.minCRI
    buffer.persistentUniqueID
    buffer.sensorManufacturer
    buffer.sensorModel
    buffer.serialNumber
    buffer.friendlyName
    buffer.sensorDescription
    buffer.connectionType

    Send buffer to Driver
}
```

## <a name="internal-methods-for-simple-sensors"></a>単純なセンサーの内部メソッド


センサー ドライバー (SPB) などの単純なセンサーをサポートする場合、データをポーリングするメソッドのサポートがあります。 擬似コードでは、このタスクの使用方法を示します、 **SpbSensorPollData**メソッド。

```cpp
datafields[] SpbSensorPollData(sensorID)
{
    // the driver is making a request for polled data, respond
    // by returning the data for this sensor synchronously to the driver

    Query newDatafields[] synchronously from the device via SPB

    return newDatafields[]
}
```

## <a name="related-topics"></a>関連トピック
[センサー ドライバー開発の基本概念](sensor-driver-development-basics.md)




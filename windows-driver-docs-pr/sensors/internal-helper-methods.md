---
title: ドライバーの更新方法
ms.assetid: F809BCE4-9176-4503-9EC7-B80AC229ABB5
description: センサー ドライバーでサポートされるメソッドを更新します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c6b99dea76757168550bb276174d27be532e4d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345194"
---
# <a name="driver-update-methods"></a>ドライバーの更新方法


センサー ドライバーには、現在のレポート間隔の更新を処理する、秘密度を変更および具合内部メソッドがサポートしています。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DriverUpdateCRI(sensorID)
-   DriverUpdateCS(sensorID)
-   DriverUpdateLDA(sensorID)
-   DriverUpdateSensorState (sensorID、状態、イベント)
-   DriverUpdateDatafields(sensorID)

## <a name="sensor-reporting-field-updates"></a>センサー レポート フィールドの更新


**DriverUpdateCRI**、 **DriverUpdateCS**、および**DriverUpdateLDA**ドライバーが、現在のレポート間隔、感度の変更を更新する方法を説明し、場所データの精度のフィールドです。

```cpp
DriverUpdateCRI(sensorID)
{
    if (true == flagCRI)
    {
        // Note that only the clients that have specified a CRI are considered
        // when determining which client has the lowest requested CRI
        Set selectedCRI of sensorID device to lowest of clientCRIs

        if (selectedCRI < effectiveMinCRI)
        {
            selectedCRI = effectiveMinCRI
        }
    }
    else //no client has specified a CRI
    {
        selectedCRI = defaultCRI
    }

    effectiveCRI = DriverUpdateSensorDeviceCRI(sensorID, selectedCRI)
}
```

```cpp
DriverUpdateCS(sensorID)
{
    for (each datafield supported by sensorID)
    {
        if (true == flagCS)
        {
            // Note that only the clients that have specified a CS are considered
            // when determining which client has the lowest requested CS
            Set selectedCS[n] of sensorID device to lowest of clientCS[n]
        }
        else //no client has specified a CS
        {
            selectedCS[n] = defaultCS[n]
        }
    }

    effectiveCS[] = DriverUpdateSensorDeviceCS(sensorID, selectedCS[])
}
```

```cpp
DriverUpdateLDA(sensorID)
{
    if (true == flagLDA)
    {
        // Note that only the clients that have specified an LDAare considered
        // when determining which client has the lowest (most accurate) requested LDA
        Set selectedLDA of sensorID device to lowest (most accurate) of clientLDAs
    }
    else //no client has specified a LDA
    {
        selectedLDA = defaultLDA
    }

    effectiveLDA = DriverUpdateSensorDeviceLDA(sensorID, selectedLDA)
}
```

## <a name="sensor-state-updates"></a>センサーの状態の更新


**DriverUpdateSensorState**メソッドは、ドライバーがセンサー イベントのレポートを更新する方法について説明し、電源の状態。

```cpp
DriverUpdateSensorState(sensorID)
{
    if (clientCount == 0) // no clients
    {
        if (subscriberCount == 0) //no subscribers
        {
            selectedRS = reportingStateNoEvents
            selectedPS = powerStatePowerOff
        }
        else //has subscribers
        {
            //illegal state
            selectedRS = reportingStateNoEvents
            selectedPS = powerStatePowerOff
        }
    }
    else //has clients
    {
        if (subscriberCount == 0) //no subscribers
        {
            if (true == flagCRI)
            {
                selectedRS = reportingStateAllEvents
                selectedPS = powerStateFullPower
            }
            else
            {
                selectedRS = reportingStateNoEvents
                selectedPS = powerStateLowPower
            }
            else

        }
        else //has subscribers
        {
            selectedRS = reportingStateAllEvents
            selectedPS = powerStateFullPower
        }
    }

    effectiveRS = DriverUpdateSensorDeviceRS(sensorID, selectedRS)
    effectivePS = DriverUpdateSensorDevicePS(sensorID, selectedPS)
}
```

## <a name="data-field-updates"></a>データ フィールドの更新


**DriverUpdateDatafields**メソッドでは、ドライバーがそのデータ フィールドを更新する方法を示します。

```cpp
DriverUpdateDatafields(sensorID)
{
    if (effectiveRS == eventsOff)
    {
        if (sensor device is intelligent (ex. HID))
        {
            HIDSensorPollData(sensorID)

            // a poll response by the sensor device will happen asynchronously
            // the sensor device responds to this poll request by sending an
            // input packed, and this is received in the
            // DriverHandleAsyncDataEvent() just as any other data packet
            // is received
        }
        else if (sensor device is simple (ex. SPB))
        {
            currentDatafields[] = SpbSensorPollData(sensorID)

            // ** TODO: Data is not updated asynchronously when polled
            // ** via SPB. Datafields[] must be assigned similarly to
            // ** DDIHandleAsyncDataEvent() when that logic has been
            // ** finalized. A shared helper method is likely best.
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
    else
    {
        // datafields are being updated by events
        // (i.e. DDIHandleAsyncDataEvent)
    }
}
```

## <a name="related-topics"></a>関連トピック
[センサー ドライバー開発の基本概念](sensor-driver-development-basics.md)




---
title: デバイスの更新方法
ms.assetid: EB5158D7-6ACA-42BB-89E2-0937EAB94BA2
description: センサー デバイスを更新するセンサー ドライバーでサポートされるメソッド。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d20b4d4e9dfe740e9a22c22c80a1d3921568435
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575057"
---
# <a name="device-update-methods"></a>デバイスの更新方法


センサー ドライバーでは、センサー デバイスを更新するメソッドをサポートします。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DriverUpdateDeviceCRI
-   DriverUpdateDeviceCS
-   DriverUpdateDeviceLDA
-   DriverUpdateDeviceRS
-   DriverUpdateDevicePS

## <a name="device-reporting-reporting-updates"></a>レポートをレポートするデバイスを更新します。


**DriverUpdateDeviceCRI**、 **DriverUpdateDeviceCS**、および**DriverUpdateDeviceLDA**メソッドは、ドライバーが現在のレポート間隔の変更を更新する方法を示します秘密度、およびデバイス上の場所データの精度フィールド。

```cpp
effectiveCRI DriverUpdateDeviceCRI(sensorID, requestedCRI)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) //Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set CRI via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectiveCRI
}
```

```cpp
effectiveCS[] DriverUpdateDeviceCS(sensorID, requestedCSs)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set CS via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectiveCS[]
}
```

```cpp
effectiveLDA DriverUpdateDeviceLDA(sensorID, requestedLDA)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set LDA via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectiveLDA
}
```

## <a name="device-interrupt-updates"></a>デバイスの割り込みの更新プログラム


**DriverUpdateDeviceRS**メソッドは、ドライバーを有効または、デバイスの割り込みを無効にする方法を示します。

```cpp
effectiveRS DriverUpdateDeviceRS(sensorID, requestedRS)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        if (requestedRS == quiescent)
        {
            Disable SPB device interrupts
        }
        else if (requestedRS == eventing)
        {
            Enable SPB device interrupts for eventing
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

    return effectiveRS
}
```

## <a name="device-power-state-updates"></a>デバイスの電源状態の更新プログラム


**DriverUpdateDevicePS**メソッドでは、ドライバーがデバイスの電源の状態を設定する方法を示します。

```cpp
effectivePS DriverUpdateDevicePS(sensorID, requestedPS)
{
    if (sensor device is intelligent (ex. HID))
    {
        HIDSensorSetProperties(sensorID, requestedRS, requestedPS, requestedCRI, requestedCS[], requestedLDA) // Driver issues USB/HID “SET_FEATURE” command to the sensor device
    }
    else if (sensor device is simple (ex. SPB))
    {
        Set power state via SPB
    }
    else if (sensor device is fusion)
    {
        //handle fusion sensor
    }
    else //is some other kind of sensor
    {
        //special action
    }

    return effectivePS
}
```

## <a name="related-topics"></a>関連トピック
[センサー ドライバー開発の基本概念](sensor-driver-development-basics.md)




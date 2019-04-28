---
title: ドライバーの初期化メソッド
ms.assetid: CA8F6308-501D-47BC-902E-3259949A1D57
description: デバイスを初期化するためにセンサー ドライバーでサポートされるメソッド。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c538a27af08030c5ab44acbf17f4e0de27ef8541
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377813"
---
# <a name="driver-initialization-methods"></a>ドライバーの初期化メソッド


センサー ドライバーでは、クライアントとデバイスの両方の初期化をサポートする必要があります。 擬似コードでは、次のメソッドを使用してこれを示しています。

-   DriverClientInitialize()
-   DeviceSensorInitialize()

## <a name="client-initialization"></a>クライアントの初期化


クライアントの初期化メソッドでは、次の形式があります。

```cpp
DriverClientInitialize(sensorID)
{
    // the following properties can be set from the API
    CRI = defaultCRI
    CS[] = defaultCS[]
    LDA = default[LDA]

    // the following properties cannot be set from the API
    // the driver provides defaults for these properties
    // the defaults can be overridden by the device
    sensorCategory = defaultSensorCategory
    sensorType = defaultSensorType
    minCRI = defaultMinCRI
    persistentUniqueID = defaultPersistentUniqueID
    sensorManufacturer = defaultSensorManufacturer
    sensorModel = defaultSensorModel
    serialNumber = defaultSerialNumber
    friendlyName = defaultFriendlyName
    sensorDescription = defaultDescription
    connectionType = defaultConnectionType

    // the following values are internal to the driver
    clientCount = 0
    subscriberCount = 0

    flagCRI = false
    flagCS = false
    flagLDA = false

    deviceState = deviceStateDisconnected
}
```

## <a name="related-topics"></a>関連トピック
[センサー ドライバー開発の基本概念](sensor-driver-development-basics.md)




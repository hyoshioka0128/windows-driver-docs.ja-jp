---
title: 加速度計プロパティをサポート
description: ソース ファイル、SensorDdi.cpp には、加速度計のデバイスでサポートされるプロパティを定義する PROPERTYKEY 構造体の 3 つの配列が含まれています。
ms.assetid: A1196CFD-9A90-479A-859E-6F9850867AC6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de24efa4a5a01149edacd664939c8aa7619865a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378568"
---
# <a name="supporting-the-accelerometer-properties"></a>加速度計プロパティをサポート


ソース ファイル、SensorDdi.cpp には、加速度計のデバイスでサポートされるプロパティを定義する PROPERTYKEY 構造体の 3 つの配列が含まれています。

最初の配列には、センサーの [全般] プロパティが含まれています。 これに製造元の名前、デバイス モデル、シリアル番号などの文字列が含まれます。 さらに、最小値と最大範囲、センサーの解像度最小のサポートされているレポートの間隔などの値があります。

```cpp
const PROPERTYKEY g_SupportedAccelerometerProperties[] =
{
    WPD_OBJECT_ID,
    SENSOR_PROPERTY_TYPE,
    SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID,
    SENSOR_PROPERTY_MANUFACTURER,
    SENSOR_PROPERTY_MODEL,
    SENSOR_PROPERTY_SERIAL_NUMBER,
    SENSOR_PROPERTY_FRIENDLY_NAME,
    SENSOR_PROPERTY_DESCRIPTION,
    SENSOR_PROPERTY_CONNECTION_TYPE,
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
    SENSOR_PROPERTY_STATE,
    SENSOR_PROPERTY_MIN_REPORT_INTERVAL,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

2 番目の配列には、3 つの特定のデバイス プロパティが含まれています: 最小値と最大範囲とセンサーの解像度。

```cpp
const PROPERTYKEY g_SupportedPerDataFieldProperties[] =
{
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
};
```

3 番目の配列には、加速度計の感度の変更と現在のレポート間隔が含まれています。

```cpp
const PROPERTYKEY g_SettableAccelerometerProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,
};
```

## <a name="related-topics"></a>関連トピック
[SpbAccelerometer ドライバーのサンプル](spbaccelerometer-driver-sample.md)




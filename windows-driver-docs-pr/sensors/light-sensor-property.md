---
title: 光センサーのプロパティ
description: 光センサーのプロパティのキー。
ms.assetid: 87C58F14-E23D-4567-BBD5-AA42DF9371B0
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 57161a83aa5e8690f2861fffc3940622d93c44cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580008"
---
# <a name="light-sensor-property"></a>光センサーのプロパティ


光センサーのプロパティのキー。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティのキー</th>
<th>型</th>
<th>アクセス (R/O、読み取り/書き込み)</th>
<th>必須/オプション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_LightSensor_ResponseCurve</p></td>
<td><p>VT_VECTOR |VT_UI4</p></td>
<td><p>R/O</p></td>
<td><p>必須</p></td>
<td><p>光センサーの応答曲線。</p></td>
</tr>
<tr class="even">
<td><p>DEVPKEY_SensorData_LightLevel_AutoBrightnessPreferred</p></td>
<td><p>VT_BOOL</p></td>
<td><p>R/O</p></td>
<td><p>省略可能</p></td>
<td><p>自動明るさの光センサーお勧めします。</p></td>
</tr>
<tr class="odd">
<td><p>DEVPKEY_SensorData_LightLevel_ColorCapable</p></td>
<td><p>VT_BOOL</p></td>
<td><p>R/O</p></td>
<td><p>任意。 一番と光の温度をサポートしている場合に必要です。</p></td>
<td><p>ライトの温度やが一番の光センサーをサポートしています x と y です。</p></td>
</tr>
</tbody>
</table>

 

表示されるデータ型の詳細については、**型**列を参照してください[PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

**注釈**

このプロパティのキーを使用すると、その関連するプロパティの値を設定するに使用することができます、 **InitPropVariantFromUInt32Vector**関数。 たとえば、センサーの値を設定する\_プロパティ\_MIN\_データ\_鍵を使用して間隔プロパティ\_センサー\_MinimumDataInterval\_Ms プロパティ キーは、します。次の構文を使用します。

```cpp
// Sensor Properties
     if (NT_SUCCESS(Status))
     {
         Status = InitSensorCollection(SENSOR_PROPERTIES_COUNT, &amp;m_pSensorProperties, SensorInstance);
         if (NT_SUCCESS(Status))
         {
               m_Interval = DEFAULT_ACCELEROMETER_REPORT_INTERVAL;
               ...
               ...
               m_pSensorProperties->List[SENSOR_PROPERTY_MIN_DATA_INTERVAL].Key = PKEY_Sensor_MinimumDataInterval_Ms;
               InitPropVariantFromUInt32(ACCELEROMETER_MIN_REPORT_INTERVAL, &amp;(m_pSensorProperties->List[SENSOR_PROPERTY_MIN_DATA_INTERVAL].Value));
               ...
         }
    }
```

関連するプロパティのキーを使用して設定するセンサー プロパティの完全な例を参照してください、 [client.cpp ファイル](https://github.com/Microsoft/Windows-driver-samples/blob/master/sensors/ADXL345Acc/client.cpp)ADXL345Acc サンプル ドライバー、および下にスクロール、 **NTSTATUS ADXL345AccDevice::Initialize (.)** ルーチン。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


**ヘッダー:** Sensorsdef.h

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[その他のセンサー プロパティ](other-sensor-properties.md)

 

 







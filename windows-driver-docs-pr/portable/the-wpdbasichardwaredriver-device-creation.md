---
Description: センサー デバイスの作成
title: センサー デバイスの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 741968915d47f5ef980e7b2327c2b9e3cba77c15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378205"
---
# <a name="creating-the-sensor-devices"></a>センサー デバイスの作成


センサーの回路は、parallax のセンサー データ シートで提供されるサンプルの回線に基づいています。 視差 BS2 プログラミング可能なマイクロ コント ローラーと各センサーの統合には、これらの回線が設計されています。

たとえば、次の図の回線とイメージ Ultrasonic 距離センサーのデータシートを示しています。

![ultrasonic 距離センサー](images/ping_datasheet.png)

この図では、ピン 15、BS2 on は、センサー データを受信します。 各センサーのファームウェアは、よく似ています。 2 つの主な機能で構成されます。PollSensor RetrieveInterval.

PollSensor 関数のコードでは、センサーからセンサーには異なります。 Ultrasonic 距離センサーの場合 PollSensor 関数は ultrasonic transducer でパルスを発行、応答を待機し、応答が発生するためにかかる時間を測定します。

```cpp
PollSensor:
  PULSOUT 15, 5
  PULSIN 15, 1, time
  cmDistance = cmConstant ** time
RETURN
```

RetrieveInterval 関数は、すべてのセンサーのと同じです。 この関数は、(1 つが送信された) 場合は、WPD ドライバーから新しい間隔のパケットを取得し、更新間隔のプロパティを適宜ファームウェアでします。 間隔は、ドライバーから受信しませんでした、RetrieveInterval 関数は、既定のタイムアウト関数を呼び出します。 この関数は、WPD ドライバーにセンサー データを送信します。

```cpp
RetrieveInterval:
    SERIN 16, 16780, Interval, Timeout, [DEC NewInterval]   'Retrieve interval
    IF NewInterval >= 10 AND NewInterval <= 60000 THEN
      Interval = NewInterval
    ENDIF
RETURN
```

タイムアウト関数は、次の形式を持ちます。

```cpp
Timeout:
  SEROUT 16, 16780, [DEC1 SensorID, DEC1 ElementSize, DEC1 ElementCount, DEC5 cmDistance, DEC5 Interval]
GOTO Main
```

タイムアウト関数を PollSensor を呼び出すメイン ルーチンに返すことに注意します。

```cpp
Main:
  GOSUB PollSensor                   'Determine distance
  GOSUB RetrieveInterval             'Retrieve interval data
```

Ultrasonic 距離センサーの完全なソース コードを次に示します。

```cpp
' Smart Sensors and Applications - PingMeasureCmAndIn.bs2
' Measure distance with Ping))) sensor and display in both in & cm
' {$STAMP BS2}
' {$PBASIC 2.5}
' Conversion constants for room temperature measurements.
CmConstant CON 2260
'InConstant CON 890
cmDistance VAR Word
'inDistance VAR Word
time VAR Word
SensorID  VAR   Byte  'Sensor identifier = 5 for PIR
ElementSize VAR Byte  'Size (in bytes) of each element
ElementCount  VAR   Byte  'Count of elements in packet
Padding VAR Byte      'Padding for the 8-byte element

SensorID = 4
ElementSize = 1
ElementCount = 5      '5bytes for distance data

NewInterval VAR  Word  'New interval requested by user
Interval  VAR   Word   'Interval value utlized by firmware

Interval = 2000
NewInterval = 2000


Main:
  GOSUB PollSensor                  'Was motion detected?
  GOSUB RetrieveInterval            'Retrieve units data

Timeout:
  SEROUT 16, 16780, [DEC1 SensorID, DEC1 ElementSize, DEC1 ElementCount, DEC5 cmDistance, DEC5 Interval]
GOTO Main

PollSensor:
  PULSOUT 15, 5
  PULSIN 15, 1, time
  cmDistance = cmConstant ** time
RETURN

RetrieveInterval:
    SERIN 16, 16780, Interval, Timeout, [DEC NewInterval]   'Retrieve interval
    IF NewInterval >= 10 AND NewInterval <= 60000 THEN
      Interval = NewInterval
    ENDIF
RETURN
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 






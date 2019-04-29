---
title: センサー HID クラス ドライバー
description: Windows オペレーティング システムには、インボックス センサー HID クラス ドライバー (SensorsHIDClassDriver.dll) が含まれています。
ms.assetid: F43958F0-5AFD-40E9-A583-FAA25F8C1B7D
keywords:
- センサー HID クラス ドライバー
- センサー HID クラス ドライバー
- HID
- HID プロトコル
- センサー ドライバーのサンプル
- センサー ドライバーでは、サンプル
- Windows 8 センサー ドライバー
- Windows 8 のセンサー ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5edeb20dbe097552c3c96b03f3f925c271d7238
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384455"
---
# <a name="sensor-hid-class-driver"></a>センサー HID クラス ドライバー


Windows 8 以降、Windows オペレーティング システムには、11 種類のセンサー HID トランスポートを使用して通信をサポートするインボックス センサー HID クラス ドライバー (SensorsHIDClassDriver.dll) が含まれています。

サポートされているセンサーの一覧を次に示します。

-   加速度計 3D
-   アンビエント ライト
-   大気温度
-   大気圧
-   コンパス 3D
-   デバイスの向き
-   3D のジャイロスコープなどがあります。
-   湿度
-   傾斜計 3D
-   プレゼンス
-   近接通信

次の図は、ドライバー スタックを経由して、最後に、ハードウェア自体に、下の 2 つのセンサー アプリケーションから前後のデータ フローを示しています。

![クライアントのセンサーのアーキテクチャ](images/client-sensor-architecture.png)

## <a name="support-for-custom-sensors"></a>カスタム センサーのサポート


だけでなく、前の一覧で説明した 11 個のセンサー クラス ドライバーには、カスタム クラスもサポートしています。 このクラスは、前のリストにないデバイスを統合するセンサー メーカーを使用できます。たとえば、一酸化炭素センサー。 カスタム センサーは自体をセンサー API カスタム デバイスとして一意のプロパティを使用します。

## <a name="architecture-and-overview"></a>アーキテクチャと概要


互換性のあるセンサーのファームウェアを作成する場合は、クラス ドライバーによってサポートされている I/O モデルの基本的な知識を必要があります。

-   センサーは、機能のレポートまたは入力のレポートのいずれかを HID クラス ドライバーに送信します。 機能のレポートは、ドライバーからの要求に対する応答で送信されます。 このレポートには、センサーの変更の区別に関する設定、そのレポート期間のレポートの状態を含むプロパティのデータが含まれています。 入力のレポートは、要求時、またはイベントへの応答で非同期的に送信されます。 このレポートには、実際のセンサー データが含まれています。 加速度計の例では、レポートが含まれています、x、y、および z 軸に沿って G フォースには)。
-   HID クラス ドライバーは、センサーの機能のレポートを送信します。 たとえば、アプリケーションでは、新しい感度の変更またはレポートの間隔を要求、ドライバーは機能レポートにこれらの値をパッケージ化し、このレポートを使用して、センサーのファームウェアを要求を送信します。

次の図は、I/O モデルを示しています。

![i/o モデル](images/hid-sensor-stack.png)

## <a name="sample-report-descriptor"></a>サンプル レポート記述子


センサー クラス ドライバーのネイティブの 7 つのカテゴリの 1 つをサポートする場合のファームウェアが特定の機能および入力をサポートする必要がありますレポートします。 機能のレポートには、センサーの現在状態、そのステータス、感度の変更、レポートおよびレポート (その他の可能なプロパティ) だけでなく間隔が含まれます。 入力のレポートには、センサー測定値が含まれます。True または False、スイッチ、または、環境光センサーの LUX の加速度計 g 値。

### <a name="sample-accelerometer-feature-report"></a>加速度計の機能のサンプル レポート

次のコード例は、加速度計の HID 機能のレポートを示しています。 このレポートの自己記述型の性質に注意してください。 これには、最小値と最大値と、カウントと個別のフィールドのサイズが含まれます。

``` syntax
//feature reports (xmit/receive)
    HID_USAGE_PAGE_SENSOR,
    HID_USAGE_SENSOR_PROPERTY_REPORTING_STATE,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_FEATURE(Data_Var_Abs),

    HID_USAGE_SENSOR_PROPERTY_SENSOR_STATUS,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_FEATURE(Data_Var_Abs),

    HID_USAGE_SENSOR_PROPERTY_CHANGE_SENSITIVITY_ABS,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_16(0xFF,0xFF), //LOGICAL_MAXIMUM (65535) 
    HID_REPORT_SIZE(16),
    HID_REPORT_COUNT(1),
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_FEATURE(Data_Var_Abs),

    HID_USAGE_SENSOR_PROPERTY_REPORT_INTERVAL,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_32(0xFF,0xFF,0xFF,0xFF), //LOGICAL_MAXIMUM (4294967295) 
    HID_REPORT_SIZE(32),
    HID_REPORT_COUNT(1),
    HID_USAGE_SENSOR_UNITS_MILLISECOND,
    HID_UNIT_EXPONENT(0), 
    HID_FEATURE(Data_Var_Abs),
```

### <a name="sample-accelerometer-input-report"></a>加速度計のサンプル入力レポート

次のコード例では、同じデバイスの HID 入力レポートを示します。 ここでも、このレポートにフィールドの自己記述型の性質に注意してください。

``` syntax
//input reports (transmit)
    HID_USAGE_PAGE_SENSOR,
    HID_USAGE_SENSOR_STATE,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_EVENT,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_ACCELERATION_X_AXIS,
    HID_LOGICAL_MIN_16(0x01,0x80),             //    LOGICAL_MINIMUM (-32767) 
    HID_LOGICAL_MAX_16(0xFF,0x7F),             //    LOGICAL_MAXIMUM (32767)
    HID_REPORT_SIZE(16), 
    HID_REPORT_COUNT(1), 
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_ACCELERATION_Y_AXIS,
    HID_LOGICAL_MIN_16(0x01,0x80),             //    LOGICAL_MINIMUM (-32767) 
    HID_LOGICAL_MAX_16(0xFF,0x7F),             //    LOGICAL_MAXIMUM (32767)
    HID_REPORT_SIZE(16), 
    HID_REPORT_COUNT(1), 
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_ACCELERATION_Z_AXIS,
    HID_LOGICAL_MIN_16(0x01,0x80),             //    LOGICAL_MINIMUM (-32767) 
    HID_LOGICAL_MAX_16(0xFF,0x7F),             //    LOGICAL_MAXIMUM (32767)
    HID_REPORT_SIZE(16), 
    HID_REPORT_COUNT(3), 
    HID_USAGE_SENSOR_UNITS_G,
    HID_UNIT_EXPONENT(0xE), 
    HID_INPUT(Data_Var_Abs),

    HID_USAGE_SENSOR_DATA_MOTION_INTENSITY,
    HID_LOGICAL_MIN_8(0x00),                   //LOGICAL_MINIMUM (0) 
    HID_LOGICAL_MAX_8(0xFF),             //LOGICAL_MAXIMUM (255) 
    HID_REPORT_SIZE(8),
    HID_REPORT_COUNT(1),
    HID_INPUT(Data_Var_Abs),
```

 

 





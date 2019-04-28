---
title: 加速度計オブジェクトの定義
description: 加速度計は、ドライバーのサンプルは、オブジェクトとして扱います。
ms.assetid: EA30C9E6-3DA1-44C8-89DA-6FA21BE3B226
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d909c42980a302e4165685af9b155ffdd68151ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377822"
---
# <a name="defining-the-accelerometer-object"></a>加速度計オブジェクトの定義


加速度計は、ドライバーのサンプルは、オブジェクトとして扱います。

## <a name="defining-the-accelerometer-object"></a>加速度計オブジェクトの定義


このオブジェクトが AccelerometerDevice.h; ヘッダー ファイルで宣言されています。また、AccelerometerDevice.cpp ソース ファイルで定義されます。 追加のセンサーをサポートするには、このドライバーを拡張した場合は、同様のヘッダーとこれらの追加のデバイスに対応するソース ファイルを作成します。 (場合に、ドライバーには、1 つのセンサーがサポートされている、置き換えてこのヘッダーとソース デバイスとその機能と要件に対応するファイルです。)

加速度計オブジェクトでメソッドをサポートします。

-   センサーのオブジェクトを初期化します。
-   ハードウェアを構成します。
-   データの通知の割り込みを接続します。
-   レポート間隔を設定します。
-   デバイスの状態を設定します。
-   デバイスの登録インターフェイスにデータを書き込む

### <a name="initializing-the-sensor-object"></a>センサーのオブジェクトの初期化

オブジェクトがサポートする、**初期化**メソッド、ACPI からデバイスの構成設定を取得し、次に、リソースのハブの接続 Id を取得します。

### <a name="configuring-the-hardware"></a>ハードウェアの構成

オブジェクトがサポートする、 **ConfigureHardware**読み取りおよび書き込みバッファーを割り当てるし、読み取りと書き込みのレジスタを設定するメソッド。

### <a name="configuring-the-data-notification-interrupt"></a>データ通知割り込みを構成します。

オブジェクトがサポートする、 **ConnectInterrupt** WUDF デバイスの割り込みを作成するメソッド。 これは構成することによって、 **WUDF\_INTERRUPT\_CONFIG**データ構造体とし、呼び出し、 **IWDFDevice3::CreateInterrupt**メソッド。

### <a name="supporting-the-report-interval"></a>レポート間隔のサポート

センサー プラットフォームのレポート期間の概念をサポートしてアプリケーションをこの間隔を定義された範囲内の値に設定できます。 Windows アプリは呼び出すことによって、加速度計の間隔を設定することができます、 **Accelerometer.ReportInterval**プロパティ。 アプリがこのプロパティは、ドライバーを呼び出すときに**SetReportInterval**デバイスのファームウェアに要求された間隔を渡すメソッドが呼び出されます。

レポート間隔を担当の主要なコンポーネントは、クライアント マネージャーです。 サポート コードには、モジュール ClientManager.cpp が記載されています。 クライアント マネージャーは、接続されているクライアント、そのサブスクリプションの状態、目的のレポート間隔、および必要な変更の感度のリストを保持します。 データ モードおよび最小のレポート間隔を更新し、秘密度値が変更されるたびに、上記の変更には、クライアント マネージャーを計算します。 レポートの間隔と変更の区別に関する詳細については、次を参照してください。、[データのフィルター処理](filtering-data.md)トピック。

ADXL345 の最小値と既定のレポート間隔は、Adxl345.h ファイルで定義されます。 ドライバーのサンプルでは、最小のレポートの間隔を 10 ミリ秒と 100 ミリ秒、間隔の既定値を制限します。

### <a name="supporting-the-device-state"></a>デバイスの状態をサポートしています。

サンプル デバイスには、3 つのモードがサポートされています。

-   イベントを測定モード
-   測定モード イベントなし
-   スタンバイ モード

測定モードは、データの収集になるモードスタンバイ モード (名前が示すように) データがデバイスによって返される結果します。 イベントを測定モードを設定すると、ドライバーは、デバイスからデータが到着する通知を受信登録するアプリを許可します。 イベントなし測定モードを設定すると、する場合、アプリは、最新のデータについては、デバイスをポーリングする必要があります。

これには 3 つのモードのそれぞれに対応するソース ファイル内の 3 つの方法があります。**SetDeviceStateEventing**、 **SetDeviceStatePolling**、および**SetDeviceStateStandby**します。 内からこれらのメソッドが呼び出される**SetDataUpdateMode**します。

### <a name="writing-data-to-the-devices-register-interface"></a>デバイスの登録インターフェイスにデータを書き込む

そのレジスタに値を記述することで、ADXL345 が制御されます。 たとえば、ドライバーが割り込みを有効に適切なビットを設定して、 **INT\_を有効にする**を登録します。 ドライバーが値を書き込む場合、特定の割り込みの暗証番号 (pin) を選択し、 **INT\_マップ**を登録します。

ドライバーでは、 **WriteRegister**をセンサー レジスタにデータを書き込むときに内部的には、呼び出すメソッド。 このメソッドの最初の引数を指定するレジスタに書き込まれた、データ バッファーと 3 番目の引数を 2 番目の引数のポイントをバッファーのサイズを指定します。

加速度計の完全な登録マップは、デバイスのデータ シートの 16 のテーブル内にあります。 ドライバーのサンプルでは、レジスタのマップ内の値のサブセットをサポートします。 これらのサポートされている値は、Adxl345.h ヘッダー ファイル内にあります。

```cpp
//
// Register interface
//

#define ADXL345_DEVID                       0x00
#define ADXL345_THRESH_TAP                  0x1D
#define ADXL345_OFFSET_X                    0x1E
#define ADXL345_OFFSET_Y                    0x1F
#define ADXL345_OFFSET_Z                    0x20
#define ADXL345_DURATION_TAP                0x21
#define ADXL345_LATENT_TAP                  0x22
#define ADXL345_WINDOW_TAP                  0x23
#define ADXL345_THRESH_ACT                  0x24
#define ADXL345_THRESH_INACT                0x25
#define ADXL345_TIME_INACT                  0x26
#define ADXL345_ACT_INACT_CTL               0x27
#define ADXL345_THRESH_FF                   0x28
#define ADXL345_TIME_FF                     0x29
#define ADXL345_TAP_AXES                    0x2A
#define ADXL345_ACT_TAP_STATUS              0x2B
#define ADXL345_BW_RATE                     0x2C
#define ADXL345_POWER_CTL                   0x2D
#define ADXL345_INT_ENABLE                  0x2E
#define ADXL345_INT_MAP                     0x2F
#define ADXL345_INT_SOURCE                  0x30
#define ADXL345_DATA_FORMAT                 0x31
#define ADXL345_DATA_X0                     0x32
#define ADXL345_DATA_X1                     0x33
#define ADXL345_DATA_Y0                     0x34
#define ADXL345_DATA_Y1                     0x35
#define ADXL345_DATA_Z0                     0x36
#define ADXL345_DATA_Z1                     0x37
#define ADXL345_FIFO_CTL                    0x38
#define ADXL345_FIFO_STATUS                 0x39
```

## <a name="related-topics"></a>関連トピック
[SpbAccelerometer ドライバーのサンプル](spbaccelerometer-driver-sample.md)




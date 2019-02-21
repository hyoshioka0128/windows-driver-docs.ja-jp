---
title: 加速度計オブジェクト
description: 加速度計は、ドライバーのサンプルは、CAccelerometerDevice クラスによって表されるオブジェクトとして扱います。
ms.assetid: D8E227E1-FFB5-4F4B-A981-6BD05C8FFAF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 256cca34dfa02bad762ebd45b930ceb8e0653a7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537819"
---
# <a name="accelerometer-object"></a>加速度計オブジェクト


| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDdi.cpp           | CSensorDdi           |

 

加速度計は、ドライバーのサンプルは、CAccelerometerDevice クラスによって表されるオブジェクトとして扱います。 このオブジェクトが AccelerometerDevice.h; ヘッダー ファイルで宣言されています。、AccelerometerDevice.cpp で定義されているとします。 ADXL345 だけでなく、別のセンサーをサポートするには、このドライバーを拡張した場合は、新しいデバイス (たとえば、CompassDevice.h および CompassDevice.cpp) に前もって同様に名前付きヘッダーとソース ファイルを作成します。 ドライバーに 1 つのセンサーがサポートされている場合は、既存のヘッダーとソース ファイルを置き換えます。

加速度計オブジェクトでメソッドをサポートします。

-   加速度計を初期化します。
    -   ハードウェアを構成します。
    -   データ通知割り込みを接続します。
    -   デバイスの登録インターフェイスにデータを書き込む
    -   デバイスの登録インターフェイスからデータを読み取る
    -   割り込みのユーザー モードをサポートします。
    -   サポートされているデータ フィールドを取得します。
    -   サポートされているイベントを取得します。
    -   サポートされているプロパティを取得します。
    -   レポート間隔を設定します。
    -   デバイスの状態を設定します。
    -   既定のプロパティ値を設定します。

## <a name="initialization-methods"></a>初期化メソッド

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

オブジェクトには、これらのメソッドがサポートされています。

| メソッド                                      | 説明                                                                                                                                                                                                                                                                           |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **CAccelerometerDevice::InitializeDevice**  | ACPI からデバイスの構成設定を取得し、次に、リソースのハブの接続 Id を取得します。 このメソッドは、 **CSensorDdi::Initialize**メソッド後者が初期化した後、センサー ドライバー インターフェイス、クライアント マネージャー、およびレポート マネージャー。 |
| **CAccelerometerDevice::ConfigureHardware** | 読み取りおよび書き込みバッファーを割り当て、読み取りと書き込みのレジスタを設定します。                                                                                                                                                                                                          |
| **CAccelerometerDevice::ConnectInterrupt**  | Sreates WUDF デバイスを中断します。 これは、WUDF を構成することによって、\_INTERRUPT\_構成データの構造体とし、呼び出し、 **IWDFDevice3::CreateInterrupt**メソッド。                                                                                                                  |

 

初期化メソッドの完全なシーケンスを参照してください、[ドライバーの初期化](driver-initialization.md)このガイドの「します。

## <a name="device-register-read--and-write-operations"></a>デバイスの登録の読み取りと書き込み操作

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

加速度計オブジェクトは、読み取りと書き込み操作の両方をサポートします。 これらの操作は、特定の登録、またはレジスタに新しい値を書き込むには、現在の値を取得するドライバーを使用できます。 **CAccelerometerDevice::ReadRegister**読み取り操作に対応して、 **CAccelerometerDevice::WriteRegister**書き込み操作に対応しています。 これらの操作が呼び出されます。

-   ドライバーの初期化に時間、 **CAccelereometerDevice::ConfigureHardware**デバイスを構成し、スタンバイ モードに配置するメソッドが呼び出されます。
-   接続されているクライアントの数がゼロになったときに、 **CAccelerometerDevice::SetDeviceStateStandby**メソッドが呼び出されます。
-   GPIO 行が、ADXL345 によってアサートされたときに、 **CAccelerometerDevice::OnInterruptIsr**メソッドが呼び出されます。

## <a name="supporting-user-mode-interrupts"></a>ユーザー モードのサポートの割り込み

このセクションでは、サンプルのドライバーが、ADXL345 のデータを取得する方法について説明します。

加速度計オブジェクトとユーザー モードの割り込みのサポート、 **CAccelerometerDevice::OnInterruptWorkItem**メソッド。 さらに、呼び出すときに、ユーザー モードのフレームワークでは、このメソッドを呼び出して、 **CAccelerometerDevice::RequestData**します。 このメソッドを呼び出す、 **CAccelerometerDevice::ReadRegister**を通じて 0x32 はレジスタの内容を読み取る、ADXL345 で 0x37 を登録します。 これら 6 つのレジスタには、g、X 軸、Y 軸、および z 軸に沿ってで現在の測定値が含まれています。

| 登録する | 目次                              |
|----------|---------------------------------------|
| 0x32     | 読み取り中の x 軸の下位バイト  |
| 0x33     | X 軸の読み取り中の高位バイト |
| 0x34     | 読み取り中の y 軸の下位バイト  |
| 0x35     | Y 軸の読み取り中の高位バイト |
| 0x36     | 読み取り中の z 軸の下位バイト  |
| 0x37     | Z 軸の読み取り中の高位バイト |

 

内のコード、 **CAccelerometerDevice::RequestData**メソッドが短い (xRaw、yRaw、および zRaw) の型の変数に各軸のレジスタの内容をパッケージ化し、.00390625 のスケール ファクターを適用します。 (スケール ファクターがの結果の高速化の範囲を分割、値 32 ここで (16 G +/-はサポートされている) ため、数で表すことができる 13 ビットで (2 ^13)-これは、選択した解決します。

```cpp
// Get the data values as doubles
SHORT xRaw, yRaw, zRaw;
DOUBLE xAccel, yAccel, zAccel;
const DOUBLE scaleFactor = 1/256.0F;

xRaw = (SHORT)((m_pDataBuffer[1] << 8) | m_pDataBuffer[0]);
yRaw = (SHORT)((m_pDataBuffer[3] << 8) | m_pDataBuffer[2]);
zRaw = (SHORT)((m_pDataBuffer[5] << 8) | m_pDataBuffer[4]);

xAccel = (DOUBLE)xRaw * scaleFactor;
yAccel = (DOUBLE)yRaw * scaleFactor;
zAccel = (DOUBLE)zRaw * scaleFactor;
```

それぞれをパッケージ化され、ドライバーが値を計算した後、 **PROPVARIANT**構造体となり、 **CAccelerometerDevice::AddDataField**各軸の値を更新するメソッド。

(16 G) +/-サポートされている高速化の範囲と解像度が、ADXL345 でレジスタ 0x31 を使用してを設定していたことに注意してください。 これが発生した、 *g\_ConfigurationSettings* AccelerometerDevice.cpp の先頭にある配列。

```cpp
// +-16g, 13-bit resolution
{ ADXL345_DATA_FORMAT,
   ADXL345_DATA_FORMAT_FULL_RES |
   ADXL345_DATA_FORMAT_JUSTIFY_RIGHT |
   ADXL345_DATA_FORMAT_RANGE_16G },
```

## <a name="supporting-the-report-interval"></a>レポート間隔のサポート

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

センサー プラットフォームでは、レポートの間隔をサポートし、アプリケーションに定義された範囲内の値に設定できます。 ドライバーのサンプルの最小値と既定のレポート間隔は、Adxl345.h ファイルで定義されます。

```cpp
const ULONG ACCELEROMETER_MIN_REPORT_INTERVAL              = 10;
const ULONG DEFAULT_ACCELEROMETER_CURRENT_REPORT_INTERVAL  = 100;
```

ドライバーのサンプルでは、最小のレポートの間隔を 10 ミリ秒と 100 ミリ秒、間隔の既定値を制限します。

センサー ドライバーでは、レポート間隔を使用して、イベント通知を発生させるタイミングを決定します。 変更の区別に達していない、ドライバーは現在の期間待機して、現在のデータの読み取りに接続されているアプリを提供するデータ イベントを発生させます。 (レポートの間隔が上書きされます。 感度の変更を超過した場合とデータ イベントをすぐに生成します。)

Windows アプリは呼び出すことによって、加速度計の間隔を設定することができます、 **Accelerometer.ReportInterval**プロパティ。 アプリがこのプロパティは、ドライバーを呼び出すときに**CAccelerometerDevice::SetReportInterval**デバイスのファームウェアに要求された間隔を渡すメソッドが呼び出されます。

レポート間隔の設定、ADXL レジスタに 3 つの連続する書き込み操作に変換します。 最初の書き込み操作は、デバイス上のデータ速度を変更して中に、割り込みを無効にします。

```cpp
// Disable interrupts while data rate is modified
pWriteBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pWriteBuffer, 1);
The second write operation updates the new data rate:

// Update the data rate.
pWriteBuffer[0] = newDataRate.RateCode;
hr = WriteRegister(ADXL345_BW_RATE, pWriteBuffer, 1);

The third write operation re-enables interrupts:

// Reenable interrupts
pWriteBuffer[0] = ADXL345_INT_ACTIVITY;
hr = WriteRegister(ADXL345_INT_ENABLE, pWriteBuffer, 1);
```

## <a name="supporting-the-device-mode"></a>デバイスのモードをサポートしています。

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

サンプル デバイスには、次の 3 つのデバイスのモードがサポートされています。

-   イベントを測定モード
-   測定モード イベントなし
-   スタンバイ モード

測定モードは、データ コレクションを結果します。スタンバイ モードでは、データがデバイスによって返される結果します。 イベントを測定モードが設定されている場合、ドライバーはアプリの登録、デバイスからデータが到着すると、通知を受信することができます。 イベントなし測定モードを設定すると、する場合、アプリは、最新のデータについては、デバイスをポーリングする必要があります。

ソース ファイル内の 3 つのメソッドは、3 つのモードのそれぞれに対応しています。**SetDeviceStateEventing、SetDeviceStatePolling**、および**SetDeviceStateStandby**します。 内から呼び出される**SetDataUpdateMode**します。

## <a name="measurement-mode-without-eventing"></a>測定モード イベントなし

Windows アプリの取得を呼び出すことによって、最新のセンサー イベントなし測定モードを設定すると、 **Accelerometer.GetCurrentReading**します。

ドライバーこのモード設定の初期化中、およびスタンバイ モードから戻るときにします。 2 つの書き込み操作を使用します。 最初の操作は、割り込みを無効にします。

```cpp
pBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

2 番目の操作では、測定モードのデバイスを配置します。

```cpp
pBuffer[0] = ADXL345_POWER_CTL_MEASURE;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

## <a name="measurement-mode-with-eventing"></a>イベントを測定モード

Windows アプリがのイベント ハンドラーを登録することで、ドライバーからデータの更新を受け取るようイベントを測定モードが設定されている場合、 **Accelerometer.ReadingChanged**イベント。

ドライバーは、初期化中に、スタンバイ モードから返されるとき) に、このモードを設定します。 ドライバーは、2 つの書き込み操作には、このモードを設定します。 最初の操作により、デバイスが測定モード内に配置されるようになります。

```cpp
pBuffer[0] = ADXL345_POWER_CTL_MEASURE;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

また、アクティビティの検出の割り込みにより、2 番目の操作。

```cpp
 pBuffer[0] = ADXL345_INT_ACTIVITY;
 hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

## <a name="supporting-standby-mode"></a>スタンバイ モードをサポートしています。

ドライバーは、クライアント サブスクリプションの数が 0 になったときに、このモードを設定します。 2 つの書き込み操作と読み取り操作を使用します。 最初の書き込み操作により、割り込みを無効にします。

```cpp
pBuffer[0] = 0;
hr = WriteRegister(ADXL345_INT_ENABLE, pBuffer, 1);
```

次に、読み取り操作の未処理の割り込みをオフにする:

```cpp
hr = ReadRegister(ADXL345_INT_SOURCE, pBuffer, 1, 0);
```

次に、2 つ目は操作の場所をスタンバイ モードで、デバイスに記述します。

```cpp
pBuffer[0] = ADXL345_POWER_CTL_STANDBY;
hr = WriteRegister(ADXL345_POWER_CTL, pBuffer, 1);
```

 

 





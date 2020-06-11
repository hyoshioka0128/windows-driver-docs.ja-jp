---
title: I2C トランスポート
description: I2C トランスポート
ms.assetid: A483FAA6-9FA6-4C91-B8D4-021DDBB9B869
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6ad66ae03f99a3d992cc470d55b443f22079681
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681674"
---
# <a name="i2c-transport"></a>I2C トランスポート


| Module                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice | CAccelerometerDevice |
| Adxl345               | 該当なし                  |

 

I ² C (IC シリーズ) トランスポートは、コンシューマー製品のために、1社によって導入された2芯のシリアル転送です。 センサーは、このトランスポートをサポートするデバイスの1つのカテゴリです。 たとえば、次のようになります。

-   ADXL345 加速度計
-   HMC5883L コンパス
-   MS5611-01BA03 大気圧センサー
-   TMP100 の温度センサー

I2C バス上の2つのワイヤは、クロックライン (SCL) とシリアルデータライン (SDA) に対応します。 I2C トランスポートの詳細については、「I2C バスの仕様」を参照してください。

I2C トランスポートをサポートするセンサーは、多くの場合、一連のレジスタをサポートしています。 マスターはこれらのレジスタを使用して、下位デバイスを構成および制御します。 ADXL345 の場合、レジスタは特定のデバイスのプロパティ、機能、または機能に対応します。 一部のレジスタは読み取り専用です。他のユーザーは読み取り/書き込み可能です。 たとえば、レジスタ 0x2D (パワー CTL) を使用すると、 \_ マスターでセンサーに自動スリープモードを設定できます。このモードでは、一定の非アクティブ状態が発生した後、デバイスが低電力状態に設定されます。 (ADXL345s レジスタとコマンドの詳細については、製造元のデータシートを参照してください)。

サンプルドライバーには、指定されたレジスタ (**CAcclelerometerDevice:: WriteRegister**) に値を書き込むメソッドと、レジスタから値を読み取るメソッド (**CAccelerometerDevicce:: readregister**) があります。 これらの引数には、書き込まれる (または読み取り元の) レジスタを識別する引数、書き込みまたは読み取りを行うデータへのポインター、およびデータバッファーのバッファーの長さを指定します。

たとえば、ドライバーとデバイスの初期化中に、次の一連の**WriteRegister**および**readregister**呼び出しが行われます。 ドライバーは**WriteRegister**を呼び出してセンサーを構成します。 操作が成功した場合、 **Readregister**は以前に書き込まれた値を反映するコンテンツを返します。

メソッドレジスタデータの目的**CAccelerometerDevice:: WriteRegister** 0x2d ' \\ 0 ' (0x00) センサーの電源管理登録をリセットし、デバイスをスタンバイモードにします。
**CAccelerometerDevice:: ReadRegister** 0x2d ' \\ 0 ' (0x00) デバイスがスタンバイモードになっています。
**CAccelerometerDevice:: WriteRegister** 0x31 ' \\ v ' (0x0b) デバイスを、+/-16g の各軸に沿った範囲で、完全解像度モードに設定します。
**CAccelerometerDevice:: ReadRegister** 0x31 ' \\ v ' (0X0b) 完全解決が最大範囲 (+/-16g) で設定されています。
. . .
. . .
. . .
 

加速度計の完全なレジスタマップは、デバイスのデータシートの表16にあります。 サンプルドライバーは、これらのレジスタのサブセットをサポートしています。 サポートされているこれらの値は、Adxl345 ヘッダーファイル内にあります。

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

 

 





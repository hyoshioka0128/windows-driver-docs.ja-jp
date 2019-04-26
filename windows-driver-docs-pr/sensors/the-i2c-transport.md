---
title: I2C トランスポート
description: I2C トランスポート
ms.assetid: A483FAA6-9FA6-4C91-B8D4-021DDBB9B869
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fab1188baaeeb4f558618ccd3914d4f31489c79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345067"
---
# <a name="i2c-transport"></a>I2C トランスポート


| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |
| Adxl345.h               | なし                  |

 

I²C (間 IC) トランスポートは、コンシューマー製品向け Phillips Corporation によって導入されたネットワーク上の 2 つのシリアル トランスポートです。 センサーは、このトランスポートをサポートするデバイスの 1 つのカテゴリです。 たとえば、次のものがあります。

-   ADXL345 加速度計
-   HMC5883L compass
-   MS5611 01BA03 気圧センサー
-   TMP100 温度センサー

I2C バスの 2 本の線は、クロック行 (SCL) およびシリアル データ行 (SDA) に対応します。 I2C トランスポートの詳細については、I2C バス仕様を参照してください。

多くの場合、I2C トランスポートをサポートするセンサーは、レジスタのセットをサポートします。 マスターは、これらのレジスタを使用して構成し、スレーブ デバイスを制御します。 ADXL345 レジスタは、特定のデバイス プロパティ、機能、または機能に対応します。 レジスタの一部は読み取り専用です。他のユーザーは、読み取り/書き込みです。 0x2D に登録できないなど、(POWER\_CTL)、センサーのことができます、マスターの設定を自動スリープ モード: このモードは、一定期間続いた後に低電力状態にデバイスを設定します。 (の詳細については、ADXL345s について登録コマンドは、製造元のデータシートを参照してください。)

ドライバーのサンプルが指定されたレジスタに値を書き込むメソッド (**CAcclelerometerDevice::WriteRegister**) もう 1 つは、レジスタの値を読み取ります (**CAccelerometerDevicce::ReadRegister**)。 優先データ バッファーに書き込まれるレジスタを識別できる (または読み取り) な引数、書き込まれるデータへのポインターまたは読み取り、およびバッファーの長さです。

たとえば、次の一連の**WriteRegister**と**ReadRegister**ドライバーとデバイスの初期化中に呼び出しを実施します。 ドライバーを呼び出す**WriteRegister**センサーを構成します。 操作が成功すると、 **ReadRegister**以前に書き込まれた値を反映する内容を返します。

登録データの目的のメソッド**CAccelerometerDevice::WriteRegister** 0x2d '\\0' (0x00)、センサーの電源管理の登録をリセットして、スタンバイ モードにデバイスを配置します。
**CAccelerometerDevice::ReadRegister** 0x2d '\\0' (0x00)、デバイスがスタンバイ モードで配置されています。
**CAccelerometerDevice::WriteRegister** 0x31 '\\v' (0x0b) は、範囲が 16 G +/-の各軸に沿ったフル解像度モードでデバイスを設定します。
**CAccelerometerDevice::ReadRegister** 0x31 '\\v' (16 G) +/-最大範囲 (0x0b) の高解像度が設定されています。
. . .
. . .
. . .
 

加速度計の完全な登録マップは、デバイスのデータ シートの表 16 でです。 ドライバーのサンプルでは、これらのレジスタのサブセットをサポートします。 これらのサポートされている値は、Adxl345.h ヘッダー ファイル内にあります。

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

 

 





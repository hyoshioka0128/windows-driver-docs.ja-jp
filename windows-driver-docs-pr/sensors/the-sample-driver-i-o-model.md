---
title: サンプルドライバーの i/o モデル
description: SPB ドライバーは、単純な周辺機器バス、システム GPIO ピン、およびリソースハブを介して通信します。 ここでは、コンポーネントがユーザーモード、カーネルモード、および実際のハードウェアでどのように構成されているかを確認できます。
ms.assetid: 86DA1BDE-DD97-45CA-884D-12BD279BD12E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b8a9c4bc1fd9be97e71729c316d515d999afa7
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681678"
---
# <a name="sample-driver-io-model"></a>サンプルドライバーの i/o モデル


SPB ドライバーは、単純な周辺機器バス、システム GPIO ピン、およびリソースハブを介して通信します。 ここでは、コンポーネントがどのように構成されているか (ユーザーモード、カーネルモード、実際のハードウェア) を確認できます。

![ドライバー i/o モデル](images/io.png)

## <a name="simple-peripheral-bus-spb"></a>SPB (Simple Peripheral Bus)


Windows 8.1 は、SPB コントローラードライバーの開発と実装を容易にするクラス拡張 (カーネルモードで実行) として SPB コンポーネントをサポートしています。 SPB コンポーネント:

-   リソースハブとのすべての通信を処理します。これには、登録や設定の取得も含まれます。
-   階層化されたキュー構造を実装して、同時ターゲットとバスロック要求を管理します
-   バッファーをユーザーモードからカーネルモードに変換します。

詳細については、「[単純な周辺機器バス](https://docs.microsoft.com/windows-hardware/design/component-guidelines/simple-peripheral-bus--spb-)」を参照してください。

### <a name="spb-component-and-the-sample-driver"></a>SPB コンポーネントとサンプルドライバー

| Module         | クラス/インターフェイス |
|----------------|-----------------|
| SpbRequest. .cpp | CSpbRequest     |

 

SpbAccelerometer サンプルコードは、SPB コンポーネントと連携しています。 次に示すように、CSpbRequest クラスの3つのメソッドは、このコンポーネントと対話します。

| Method                                          | 目的                                       |
|-------------------------------------------------|-----------------------------------------------|
| **CSpbRequest:: CreateAndSendIoctl**             | IOCTL 要求を作成して発行します。          |
| **CSpbRequest:: CreateAndSendWrite**             | SPB 書き込みを作成および発行します。               |
| **CSpbRequest:: CreateAndSendWriteReadSequence** | SPB 書き込み/読み取りシーケンスを作成して発行します。 |

 

## <a name="general-purpose-inputoutput-gpio"></a>汎用入力/出力 (GPIO)

Windows 8.1 は、カーネルモード SPB コンポーネントと同じレベルに存在する GPIO クラス拡張機能をサポートしています。 拡張機能を使用すると、基盤となるハードウェア接続と GPIO の場所を柔軟に管理でき、クライアントドライバーの標準インターフェイスが提供されます。

SoC のプラットフォームでは、GPIO ピンはチップ全体に分散され、SPI 接続モデムなどの他のコンポーネントでも公開されます。

### <a name="the-gpio-component-and-the-sample-driver"></a>GPIO コンポーネントとサンプルドライバー

| Module               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer asl | 該当なし             |

 

SpbAccelerometer サンプルは、割り込み用の GPIO コンポーネントに依存しています。 SpbAccelerometer ファイルの GpioInt () 要素は、割り込みリソースとして ADXL345 に接続されている GPIO pin を定義します。

```cpp
//
// Sample I2C and GPIO resources. Modify to match your
// platform's underlying controllers and connections.
// \_SB.I2C and \_SB.GPIO are paths to predefined I2C
// and GPIO controller instances.
//
// Note: as written SpbAccelerometer requires a GPIO resource.
//
I2CSerialBus(0x1D, ControllerInitiated, 400000, AddressingMode7Bit, "\\_SB.I2C", , )
GpioInt(Level, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPIO") {1} })
```

次に、I2C リソースの主な要素を示します。

| 要素    | 説明                                             |
|------------|---------------------------------------------------------|
| 0x1D       | 下位デバイスの I2C アドレスを指定します。         |
| 400000     | 下位デバイスの動作頻度を指定します。 |
| \\\\SB.I2C | 下位デバイスの ACPI ノードを指定します。           |

 

### <a name="processing-acceleration-data"></a>高速化データを処理しています

| Module                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice | CAccelerometerDevice |

 

ADXL345 によって GPIO 行がアサートされると、サンプルドライバーのパッシブ ISR ルーチン (**CAccelerometerDevice:: OnInterruptIsr**) が呼び出されます。 ヘルパー関数**CAccelerometerDevice:: OnInterruptWorkItem**は、::**OnInterruptIsr**に格納されている割り込みデータを処理します。

::**OnInterruptIsr**によって処理された割り込みが register 0X30 ( \_ Adxl345 ファイルの adxl 345 INT SOURCE) に対応する場合 \_ \_ 、ドライバーは、レジスタ読み取り操作を呼び出して、0x37 を介してレジスタの内容を取得します。 これらのレジスタには、X、Y、Z 軸の最新のアクセラレーションデータが含まれています。 読み取り操作は、 **CAcclerometerDevice:: RequestData**メソッド ( **CAccelerometerDevice:: OnInterruptWorkItem**によって呼び出されます) で呼び出されます。

::**Requestdata**メソッドは、読み取り操作の結果を処理するときに、最初に各軸に対応する2バイトのデータを結合します。 次に、スケールファクターを適用して、実際の加速度値を取得します。 (スケールファクターは、G-力の範囲 (32) を解像度 (2 ^ 13) で除算した結果です。 結果は. 00390625 です。)

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

スケールファクターは、レジスタ 0x31 (データ形式) の設定によって決まり \_ ます。

## <a name="resource-hub"></a>リソースハブ

Windows 8.1 は、すべてのデバイスとバスコントローラーの接続を管理するリソースハブをサポートしています。 これにより、必要な開始と停止の順序が維持されます。

ハブは、SoC プラットフォームとそのフラットデバイスツリーを対象としたコンポーネントです。 これらのシステムのバスは Pc とは異なります。

-   通常、接続は検出できません。ACPI では静的に定義されています。
-   多くの場合、ハードウェアコンポーネントは、厳密な親子関係ではなく、複数のバスにまたがる複数の依存関係を持ちます。

### <a name="resource-hub-and-the-sample-driver"></a>リソースハブとサンプルドライバー

| Module               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer asl | 該当なし             |

 

SpbAccelerometer の**Resourcetemplate**セクションでは、リソースの接続方法を指定します。

```cpp
Name(RBUF, ResourceTemplate()
{
   //
    // Sample I2C and GPIO resources. Modify to match your
    // platform's underlying controllers and connections.
    // \_SB.I2C and \_SB.GPIO are paths to predefined I2C
    // and GPIO controller instances.
    //
    // Note: as written SpbAccelerometer requires a GPIO resource.
    //
    I2CSerialBus(0x1D, ControllerInitiated, 400000, AddressingMode7Bit, "\\_SB.I2C", , )
    GpioInt(Level, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPIO") {1}
        })
Return(RBUF)
```

 

 





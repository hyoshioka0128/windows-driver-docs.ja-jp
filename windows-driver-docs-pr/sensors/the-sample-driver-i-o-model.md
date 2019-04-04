---
title: I/O ドライバー モデルのサンプル
description: SPB、ドライバーは、シンプルな周辺機器バス、システムの GPIO ピン、およびリソース ハブ経由で通信します。 ここでは、ユーザー モード、カーネル モード、および実際のハードウェア コンポーネントの編成方法を確認できます。
ms.assetid: 86DA1BDE-DD97-45CA-884D-12BD279BD12E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07e090668c678b8ad9b6f31822341acadef2b2c7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348651"
---
# <a name="sample-driver-io-model"></a>I/O ドライバー モデルのサンプル


SPB、ドライバーは、シンプルな周辺機器バス、システムの GPIO ピン、およびリソース ハブ経由で通信します。 内のコンポーネントを整理する方法を確認できます。 ユーザー モード、カーネル モード、および実際のハードウェア。

![ドライバーの i/o モデル](images/io.png)

## <a name="simple-peripheral-bus-spb"></a>SPB (Simple Peripheral Bus)


Windows 8.1 では、開発と SPB コント ローラー ドライバーを簡単に実装するクラス拡張 (カーネル モードで実行されている) として、SPB コンポーネントをサポートします。 SPB コンポーネント:

-   登録設定の取得などのリソース ハブでのすべての通信を処理します。
-   同時のターゲットとバスのロック要求を管理する implements 階層化キューの構造体
-   ユーザー モードからカーネル モードのバッファーを変換します。

詳細については、[シンプルな周辺機器のバス](https://docs.microsoft.com/windows-hardware/design/component-guidelines/simple-peripheral-bus--spb-)を参照してください。

### <a name="spb-component-and-the-sample-driver"></a>SPB コンポーネントとドライバーのサンプル

| モジュール         | クラス/インターフェイス |
|----------------|-----------------|
| SpbRequest.cpp | CSpbRequest     |

 

サンプル コード、SPB コンポーネントとやり取りする SpbAccelerometer SpbRequest.cpp はあります。 CSpbRequest クラスでは、3 つのメソッドは、以下に示すように、このコンポーネントと対話します。

| メソッド                                          | 目的                                       |
|-------------------------------------------------|-----------------------------------------------|
| **CSpbRequest::CreateAndSendIoctl**             | 作成し、IOCTL 要求を発行します。          |
| **CSpbRequest::CreateAndSendWrite**             | 作成し、書き込みを SPB の問題               |
| **CSpbRequest::CreateAndSendWriteReadSequence** | 作成し、SPB シーケンスの書き込みと読み取りを発行します。 |

 

## <a name="general-purpose-inputoutput-gpio"></a>汎用入力/出力 (GPIO)

Windows 8.1 では、カーネル モード SPB のコンポーネントと同じレベルに配置されている、GPIO のクラスの拡張機能をサポートします。 ドライバーのクライアントの標準的なインターフェイスを提供しつつ、基になるハードウェアの接続と GPIO の場所の柔軟性を高めるため、拡張を使用できます。

SoC の GPIO ピンのプラットフォームは、チップに分散だけでなく SPI に接続されたモデムのようなその他のコンポーネントで公開されています。

### <a name="the-gpio-component-and-the-sample-driver"></a>GPIO コンポーネントとドライバーのサンプル

| モジュール               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer.asl | N/A             |

 

SpbAccelerometer サンプルは、割り込みの GPIO コンポーネントに依存します。 SpbAccelerometer.asl ファイル GpioInt() 要素は、割り込みリソースとして ADXL345 に接続されている GPIO ピンを定義します。

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

I2C リソースの主な要素を次に示します。

| 要素    | 説明                                             |
|------------|---------------------------------------------------------|
| 0x1D       | スレーブ デバイス I2C アドレスを指定します。         |
| 400000     | スレーブ デバイスの動作の頻度を指定します。 |
| \\\\SB します。I2C | スレーブ デバイス ACPI ノードを指定します。           |

 

### <a name="processing-acceleration-data"></a>高速化データの処理

| モジュール                  | クラス/インターフェイス      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |

 

GPIO 行が ADXL345、サンプル ドライバーのパッシブ ISR ルーチンによってアサートされた場合 (**CAccelerometerDevice::OnInterruptIsr**) が呼び出されます。 ヘルパー関数の場合、 **CAccelerometerDevice::OnInterruptWorkItem**、割り込みのデータを処理する::**OnInterruptIsr**格納されています。

によって、割り込みが処理された場合::**OnInterruptIsr** 0x30 の登録に対応しています (ADXL\_345\_INT\_Adxl345.h ファイル内のソース)、ドライバーが、レジスタの読み取りを取得する操作を呼び出す、0x32 0x37 経由のレジスタの内容。 これらのレジスタには、x、Y 軸、および z 軸の高速化の最新データが含まれます。 読み取り操作が呼び出される、 **CAcclerometerDevice::RequestData**メソッド (によって呼び出される**CAccelerometerDevice::OnInterruptWorkItem**)。

ときに、::**RequestData**メソッドの処理、読み取り操作の結果、各軸に対応するデータの 2 バイトが最初に組み合わされています。 次に、実際の高速化の値を取得するスケール ファクターが適用されます。 (スケール ファクターは解像度の範囲の G は、強制的に (32) で除算した結果 (2 ^13)。 結果は、.00390625.).

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

スケール ファクターは 0x31 の登録の設定によって決まります (データ\_形式)。

## <a name="resource-hub"></a>リソース ハブ

Windows 8.1 には、すべてのデバイスおよびバス コント ローラーへの接続を管理するリソース ハブがサポートしています。 確実に必要な開始と停止の順序を維持します。

ハブは、SoC プラットフォームとそのフラット デバイス ツリーにある目的に特化したコンポーネントです。 これらのシステム バスは、Pc と異なります。

-   接続が通常検出不可能です;ACPI で静的に定義されています。
-   ハードウェア コンポーネントに多くの場合、厳密な親子のリレーションシップで複数バスではなくにまたがる複数の依存関係があります。

### <a name="resource-hub-and-the-sample-driver"></a>リソースのハブとドライバーのサンプル

| モジュール               | クラス/インターフェイス |
|----------------------|-----------------|
| SpbAccelerometer.asl | N/A             |

 

**ResourceTemplate** SpbAccelerometer.asl のセクションでは、リソースの接続方法を指定します。

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

 

 





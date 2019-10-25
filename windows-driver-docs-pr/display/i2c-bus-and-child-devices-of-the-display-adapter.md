---
title: ディスプレイアダプターの I2C バスおよび子デバイス
description: ディスプレイアダプターの I2C バスおよび子デバイス
ms.assetid: bfa81f2d-dc35-4430-9117-4706a446058c
keywords:
- ビデオミニポートドライバー WDK Windows 2000、I2C
- I2C WDK ビデオミニポート
- 子デバイス WDK ビデオミニポート
- I2CRead
- I2CWrite
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d915fa5b88e9096b417e9f92d8688e73cd255d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839654"
---
# <a name="i2c-bus-and-child-devices-of-the-display-adapter"></a>ディスプレイアダプターの I2C バスおよび子デバイス


## <span id="ddk_i2c_bus_and_child_devices_of_the_display_adapter_gg"></span><span id="DDK_I2C_BUS_AND_CHILD_DEVICES_OF_THE_DISPLAY_ADAPTER_GG"></span>


ディスプレイアダプターは通常、I ² C バスを介して子デバイスと通信します。 たとえば、モニターはディスプレイアダプターの子デバイスであり、ディスプレイアダプターは、すべての標準モニタケーブルに組み込まれている I2C バス経由でモニタの機能情報を読み取ることができます。

I ² C バスには、シリアルクロックラインとシリアルデータ線の2つのワイヤしかありません。 データは一度に1ビットずつ読み取られ、行に書き込まれます。 ディスプレイアダプターの I ² C 行へのデータビットの読み取りと書き込みはハードウェアに依存しているため、ベンダーが提供するビデオミニポートドライバーは、ディスプレイアダプターに対して個々のビットの読み取りと書き込みを行うように指示する機能を提供する必要があります。

## <a name="i2c-functions"></a>I2C 関数

ビデオミニポートドライバーによって実装される次の関数は、I ² C シリアルクロックとデータ行に個々のデータビットを読み書きします。

* [**ReadClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_read_clock_line)
* [**ReadDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_read_data_line)
* [**WriteClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_write_clock_line)
* [**WriteDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_write_data_line)

上記の関数は、ビデオポートドライバーの[Videoportddcmonitorhelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportddcmonitorhelper)関数を呼び出すビデオミニポートドライバーによって実装される必要があります。

VideoPortDDCMonitorHelper は、I2C 仕様に従ってモニターの拡張されたディスプレイ識別データ (EDID) を読み取るための詳細を実装しますが、読み取りと書き込みを行うには、ビデオミニポートドライバーによって実装される次の関数に依存する必要があります。個々のデータビットを I2C シリアルクロックとシリアルデータ行にします。

ビデオミニポートドライバーによって実装される*HwVidGetChildDescriptor*関数は、特定のモニターから拡張表示識別データ (edid) 構造を読み取り、edid をビデオポートドライバーに返す役割を担います。 *HwVidGetChildDescriptor*は、 **Videoportddcmonitorhelper**を呼び出して、ビデオポートドライバーからサポートを受けることができます。このヘルパーは、ディスプレイデータチャネル (DDC) 標準に従って、I ² C バスを使用してモニターの EDID を読み取ります。 ただし、 **Videoportddcmonitorhelper**が I ²の C クロックとデータ行に対して個々のビットを読み書きする必要がある場合は、ビデオミニポートドライバーにコールバックする必要があります。 したがって、 *HwVidChildDescriptor*は*I2CCallbacks*構造体 ( *readclockline*、 *Writeclockline*、 *ReadDataLine*、および*WriteDataLine*へのポインターを含む) をに**渡します。VideoPortDDCMonitorHelper**。

## <a name="i2c-functions-implemented-by-the-video-port-driver"></a>ビデオポートドライバーによって実装される I2C 関数

I ² C 仕様は、i ² c 通信を開始するためのプロトコルを定義し、I ² C データ行の読み取りと書き込みを行い、i ² C 通信を終了します。 システムによって提供されるビデオポートドライバーは、そのプロトコルを実装する次の機能を提供します。

* [**I2CStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_start)
* [**I2CRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_read)
* [**I2CWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_write)
* [**I2CStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pi2c_stop)

前の一覧の各関数 (ビデオポートドライバーによって実装されていますが、エクスポートされません) は、ビデオミニポートドライバーのサポートを必要とします。 ビデオミニポートドライバーが I ² C 関数を呼び出すことができるようにするには、VideoPortServicesI2C を[Videoportqueryservices](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices)関数に渡すことによって関数ポインターを取得する必要があります。

たとえば、 **I2CRead**関数は、I ² C データ行のバイトシーケンスを読み取ります。ただし、各バイトを読み取るには、8つの個別ビットを読み取る必要があります。これは、ビデオミニポートドライバーだけが実行できるタスクです。 **I2CRead**関数はビデオミニポートドライバーからサポートを受けることができます。これは、ビデオミニポートドライバー (*readclockline*、 *によって実装される4つの I ² C 関数に対して (I2CCallbacks 構造の) ポインターを受信するためです。WriteClockLine*、 *ReadDataLine*、および*WriteDataLine*)。 同様に、 **I2CStart**、 **I2CRead**、 **I2CWrite**はそれぞれ、4つのビデオミニポートドライバーの I ² C 関数すべてへのポインターを含む*I2CCallbacks*構造体を受け取ります。


すべてのビデオミニポートドライバーの機能の概要とそれらの機能の登録方法については、「[ビデオミニポートドライバーの機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/)」を参照してください。

I ² C バスの詳細については、「私² C バス仕様」を参照してください。

 

 






---
title: ディスプレイ アダプターの I2C バスおよび子デバイス
description: ディスプレイ アダプターの I2C バスおよび子デバイス
ms.assetid: bfa81f2d-dc35-4430-9117-4706a446058c
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、I2C
- I2C WDK ビデオのミニポート
- 子デバイス WDK のビデオのミニポート
- I2CRead
- I2CWrite
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9086af04553950c41032b30f28867c13319c0ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380198"
---
# <a name="i2c-bus-and-child-devices-of-the-display-adapter"></a>ディスプレイ アダプターの I2C バスおよび子デバイス


## <span id="ddk_i2c_bus_and_child_devices_of_the_display_adapter_gg"></span><span id="DDK_I2C_BUS_AND_CHILD_DEVICES_OF_THE_DISPLAY_ADAPTER_GG"></span>


ディスプレイ アダプターは、通常、I²C バス経由で子デバイスと通信します。 たとえば、モニターは、ディスプレイ アダプターの子デバイスとディスプレイ アダプターは、すべての標準的なモニター ケーブルに組み込まれている I2C バス経由でモニターの機能の情報を読み取ることができます。

I²C バスが 2 つだけのワイヤ: シリアル クロック行とシリアル データの行。 データはから読み取られ、行 1 のビットに一度に書き込まれます。 読み取りと書き込みデータ ビットをディスプレイ アダプターで I²C 行はハードウェアに依存する場合は、ベンダーから提供されたビデオのミニポート ドライバーは、個々 のビットを読み書きするディスプレイ アダプターを指示する機能を提供する必要があります。

## <a name="i2c-functions"></a>I2C 関数

ビデオのミニポート ドライバーで実装されている、次の関数では、読み取りし、個々 のデータ ビットを I²C シリアル時計とデータ行に書き込みます。

* [**ReadClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_read_clock_line)
* [**ReadDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_read_data_line)
* [**WriteClockLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_write_clock_line)
* [**WriteDataLine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_write_data_line)

呼び出すのビデオ ポート ドライバーのビデオのミニポート ドライバーが前の関数を実装する必要[VideoPortDDCMonitorHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportddcmonitorhelper)関数。

モニターの読み取りの詳細の拡張 VideoPortDDCMonitorHelper 実装は I2C 仕様では、id データ (EDID) を表示しますが、読み取りし、書き込みに、ビデオのミニポート ドライバーによって実装される、次の関数に依存する必要があります。I2C シリアル クロックとデータのシリアル ラインに個々 のデータ ビットです。

*HwVidGetChildDescriptor*ビデオのミニポート ドライバーによって実装される関数は、特定のモニタから強化された Display Identification Data (EDID) 構造の読み取りとビデオへの EDID を返す担当ポートのドライバーです。 *HwVidGetChildDescriptor*ビデオ ポート ドライバーから呼び出すことによって支援を受けられる**VideoPortDDCMonitorHelper**、読み取り、表示データ チャネル (DDC) 標準に従ってモニターの EDID I²C バスを使用します。 ただし、 **VideoPortDDCMonitorHelper**読み取りし、書き込みのについては、ビデオのミニポート ドライバーに戻るに呼び出す必要があります個別のビットを I²C 時計とデータの行をする必要があります。 そのため、 *HwVidChildDescriptor*渡します、 *I2CCallbacks*構造 (へのポインターを含む*ReadClockLine*、 *WriteClockLine*、 *ReadDataLine*、および*WriteDataLine*) に**VideoPortDDCMonitorHelper**します。

## <a name="i2c-functions-implemented-by-the-video-port-driver"></a>ビデオ ポート ドライバーによって実装される I2C 関数

I²C 仕様には、I²C 通信を開始する、読み取りと I²C データ行の上のバイトの書き込みおよび I²C 通信の終了のためのプロトコルが定義されています。 システム提供のビデオ ポート ドライバーでは、そのプロトコルを実装する次の機能を提供します。

* [**I2CStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_start)
* [**I2CRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_read)
* [**I2CWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_write)
* [**I2CStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pi2c_stop)

各 (実装される、ビデオ ポート ドライバーによってエクスポートされませんでしたが)、前の関数の一覧、ビデオのミニポート ドライバーからのサポートが必要です。 VideoPortServicesI2C に渡すことで関数ポインターを取得する必要があります、ビデオのミニポート ドライバーでは、I²C 関数を呼び出すことができます、前に、 [VideoPortQueryServices](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueryservices)関数。

たとえば、 **I2CRead**関数が I²C データ回線では、バイトのシーケンスを読み取りますが、各バイトを読み取るには、8 個の個別ビット、ビデオのミニポート ドライバーのみを実行できるタスクの読み取りが必要です。 **I2CRead**関数は、ポインターを受け取るために、ビデオのミニポート ドライバーからの支援を得ることができます (で、 *I2CCallbacks*構造) にビデオのミニポートによって実装される 4 つの I²C 関数ドライバー (*ReadClockLine*、 *WriteClockLine*、 *ReadDataLine*、および*WriteDataLine*)。 同様に、 **I2CStart**、 **I2CRead**、および**I2CWrite**各受信、 *I2CCallbacks*の 4 つすべてへのポインターを含む構造体ビデオのミニポート ドライバーの I²C 関数。


すべてのビデオのミニポート ドライバー機能の概要とそれらの関数を登録する方法は、次を参照してください。[ビデオのミニポート ドライバー機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/)します。

詳細 I²C バスについては、Philips 半導体によって公開されている I²C Bus 仕様を参照してください。

 

 






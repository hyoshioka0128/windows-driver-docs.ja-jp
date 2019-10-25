---
title: GPIO ドライバー サポートの概要
description: Windows 8 以降では、GPIO フレームワーク拡張機能 (GpioClx) により、GPIO コントローラー デバイス用のドライバーを記述するタスクが簡略化されます。
ms.assetid: 450E7F80-D9AC-4F52-8062-2DA5343C8D0F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee1ea09b4833c16128415229f014973f61d5139
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824990"
---
# <a name="gpio-driver-support-overview"></a>GPIO ドライバー サポートの概要


Windows 8 以降では、GPIO フレームワーク拡張機能 (GpioClx) により、GPIO コントローラー デバイス用のドライバーを記述するタスクが簡略化されます。 さらに、GpioClx により、GPIO ピンに接続される周辺機器に対してドライバー サポートが提供されます。 カーネル モード ドライバー フレームワーク (KMDF) のシステム提供の拡張機能である GpioClx では、GPIO デバイス クラスのメンバーに共通す処理タスクが実行されます。

この概要では、次のトピックについて説明します。

- [GPIO ドライバー サポートの概要](#gpio-driver-support-overview)
    - [GPIO コントローラードライバー](#gpio-controller-drivers)
    - [GPIO Pin を使用する周辺機器のドライバー](#drivers-for-peripheral-devices-that-use-gpio-pins)

## <a name="gpio-controller-drivers"></a>GPIO コントローラードライバー


ハードウェアベンダーは、GPIO コントローラーを制御するためのドライバーを提供します。 GPIO コントローラードライバーは、GPIO コントローラーのハードウェア固有のすべての操作を管理する KMDF ドライバーです。 GPIO コントローラードライバーは、データ入力とデータ出力として構成されている GPIO ピンのグループの i/o 要求を処理するために、GpioClx と連携して動作します。 さらに、このドライバーは GpioClx と連携して、割り込み入力として構成されている GPIO ピンからの割り込み要求を処理します。

GPIO コントローラーデバイスには、いくつかの GPIO ピンがあります。 これらの pin は、周辺機器に物理的に接続できます。 GPIO ピンは、データ入力、データ出力、または割り込み要求入力として構成できます。 通常、GPIO ピンは周辺機器専用であり、2つ以上のデバイスで共有されることはありません。 GPIO ピンと周辺機器の接続は固定されており、ユーザーが変更することはできません (たとえば、周辺機器を取り外して別のデバイスに置き換えるなど)。 このため、周辺機器への GPIO ピンの割り当てについては、プラットフォームのファームウェアで説明されています。




次の図は、GPIO コントローラードライバーと GpioClx を示しています。

![gpio コンポーネントのブロック図](images/gpiomodules.png)

GPIO コントローラードライバーと GpioClx は、GpioClx device driver interface (DDI) を介して相互に通信します。 GPIO コントローラードライバーは、GpioClx によって実装された[ドライバーサポートメソッド](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))を呼び出します。 GpioClx は、GPIO コントローラードライバーによって実装されている[イベントコールバック関数](https://docs.microsoft.com/previous-versions/hh439464(v=vs.85))を呼び出します。

GPIO コントローラードライバーは、GPIO コントローラーデバイスのハードウェアレジスタに直接アクセスします。

GpioClx は、物理的に GPIO ピンに接続する周辺機器のドライバーから i/o 要求を処理します。 GpioClx は、これらの i/o 要求を単純なハードウェア操作に変換します。これは、GPIO コントローラードライバーによって実装されているイベントコールバック関数を呼び出すことによって実行されます。 たとえば、GPIO ピンのセットに対してデータの読み取りまたは書き込みを行う場合、GpioClx は、[*クライアント\_ReadGpioPins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins)や[*client\_writegpiopins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)などのイベントコールバック関数を呼び出します。 GpioClx は、GPIO コントローラーの i/o キューを管理するため、このタスクの GPIO コントローラードライバーは解放されます。

さらに、GpioClx は、GPIO コントローラーデバイスからのプライマリ割り込みを処理し、これらの割り込みを、周辺機器ドライバーによって処理される2次割り込みにマップします。 プライマリ割り込みは、ハードウェアデバイスによって生成される割り込みです。 2次割り込みは、特定のプライマリ割り込みに応答してオペレーティングシステムによって生成されます。 プライマリとセカンダリの両方の割り込みは、グローバルシステム割り込み (GSIs) によって識別されます。 ハードウェアプラットフォームの ACPI ファームウェアによって GSIs がプライマリ割り込みに割り当てられ、実行時にオペレーティングシステムによってセカンダリ割り込みに GSIs が割り当てられます。

たとえば、ファームウェアによって、GPIO コントローラーからハードウェア割り込みに GSI が割り当てられ、オペレーティングシステムによって、割り込み入力として構成されている GPIO pin に GSI が割り当てられます。

GpioClx は、ハードウェアによって生成される、GPIO コントローラーデバイスからのプライマリ割り込みを処理する ISR を実装します。 周辺機器が GPIO ピンの割り込みをアサートし、このピンの割り込みが有効になり、マスクが解除された場合、GPIO コントローラーはプロセッサを中断します。 応答として、カーネルトラップハンドラーは、実行する GpioClx ISR をスケジュールします。 割り込みの原因となった GPIO ピンを識別するために、GpioClx ISR は[*クライアント\_QueryActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)イベントコールバック関数を呼び出します。これは、gpio コントローラードライバーによって実装されています。 次に、GpioClx ISR は、この pin に割り当てられている GSI を検索し、この GSI をハードウェアアブストラクションレイヤー (HAL) に渡します。 この GSI に登録されている ISR を呼び出すことによって、HAL は2次割り込みを生成します。 この ISR は、最初に割り込みをアサートした周辺機器のドライバーに属しています。

プライマリとセカンダリの割り込みの詳細については、「 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)」を参照してください。

## <a name="drivers-for-peripheral-devices-that-use-gpio-pins"></a>GPIO Pin を使用する周辺機器のドライバー


起動時に、プラグアンドプレイ (PnP) マネージャーは、PnP デバイスと非 PnP デバイスの両方を列挙します。 GPIO ピンへの接続が固定されている非 PnP デバイスの場合、PnP マネージャーはプラットフォームファームウェアに問い合わせ、これらのデバイスにシステムで管理されているハードウェアリソースとして割り当てられている GPIO pin を判別します。

周辺機器の KMDF ドライバーは、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック中に割り当てられたハードウェアリソースを受け取ります。 これらのリソースには、データ出力、データ入力、または割り込み要求入力として構成されている GPIO ピンが含まれる場合があります。

GPIO i/o リソースは、Windows 8 の新しい Windows リソースの種類です。 このリソースは、データ入力またはデータ出力として使用できる1つ以上の GPIO ピンのセットで構成されます。 周辺機器ドライバによって読み取り用の GPIO i/o リソースが開かれた場合、ドライバーはリソース内のすべてのピンをデータ入力として使用します。 ドライバーが書き込み用に GPIO i/o リソースを開くと、ドライバーはリソース内のすべてのピンをデータ出力として使用します。 周辺機器ドライバーが一連の GPIO i/o pin への論理接続を開く方法を示すコード例については、次のトピックを参照してください。

[KMDF ドライバーを GPIO i/o ピンに接続する](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

割り込み入力として構成されている GPIO pin は、通常の Windows 割り込みリソースとしてドライバーに割り当てられます。 割り込みリソースの抽象化は、割り込みがプログラム可能な割り込みコントローラーなど、GPIO pin によって実装される可能性があることを隠します。 このため、ドライバーは、他の割り込みリソースと同じように、GPIO ベースの割り込みリソースを扱うことができます。

GPIO i/o リソースの GPIO ピンにアクセスするには、周辺機器ドライバーがピンへの論理接続を開く必要があります。 KMDF ドライバーは、 [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)メソッドを呼び出して接続を開きます。 この接続を使用して、ドライバーは GPIO ピンに i/o 要求を送信できます。 ドライバーは、これらの pin (入力ピンの場合) または[**ioctl\_GPIO\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)(出力ピンの場合) へのデータの書き込み要求を書き込むために、[**読み取り\_ピン\_\_GPIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)を送信します。

割り込みリソースの GPIO ピンから割り込みを受け取るには、周辺機器ドライバーが、この pin によって実装されている割り込みリソースから割り込みを受信するように、その割り込みサービスルーチン (ISR) を登録する必要があります。 KMDF ドライバーは、 [**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドを呼び出して、ISR を割り込みに接続します。 

 

 





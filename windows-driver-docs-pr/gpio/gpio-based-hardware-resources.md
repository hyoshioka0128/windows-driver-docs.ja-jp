---
title: GPIO ベースのハードウェア リソース
description: Windows 8 以降では、GPIO コントローラーのドライバーによって制御される汎用 I/O (GPIO) ピンは、システムで管理されるハードウェア リソースとして他のドライバーで使用できます。
ms.assetid: 03A6ACDF-8BB7-40C0-A331-7F61F48A44DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdccf2d2748cc9d912f99d396e32d77031381ca5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825050"
---
# <a name="gpio-based-hardware-resources"></a>GPIO ベースのハードウェア リソース


Windows 8 以降では、GPIO コントローラーのドライバーによって制御される汎用 I/O (GPIO) ピンは、システムで管理されるハードウェア リソースとして他のドライバーで使用できます。 データ入力またはデータ出力として構成されているピンである GPIO I/O ピンは、新しい種類の Windows リソースである *GPIO I/O リソース*として使用できます。 さらに、割り込み要求の入力として構成されているピンである GPIO 割り込みピンは、通常の Windows 割り込みリソースとして使用できます。

GPIO i/o リソースは、周辺機器のドライバーで読み取りまたは書き込みができる1つ以上の GPIO ピンのセットを表します。 Windows では、GPIO i/o ピンの基礎となる実装に関する詳細が表示されないため、周辺機器ドライバーを作成して、抽象 GPIO i/o リソースを操作できます。 これらの抽象リソースを使用する周辺機器ドライバーは、リソースを実装する GPIO コントローラーハードウェアに関係なく、複数のプラットフォームで動作することがあります。 GPIO i/o リソースは、基になる GPIO ピンまたは pin を所有する特定の GPIO コントローラードライバーにこのリソースを関連付ける WDFIOTARGET ハンドルによって表されます。

通常、GPIO コントローラーの i/o ピンは、コントローラーハードウェアの機能や、pin に物理的に接続されているデバイスの機能に応じて、入力または出力用に構成できます。 このため、ドライバーは書き込み操作または読み取り操作のためにこの pin への論理接続を開くことができますが、両方を開くことはできません。 ただし、この制約は、GPIO framework 拡張機能 (GpioClx) ではなく、ハードウェアによって課せられます。 ハードウェアで i/o pin を入力と出力の両方に構成できる場合、GpioClx を使用すると、ドライバーは読み取りと書き込みの両方の操作で pin への論理接続を開くことができます。

割り込み要求入力として構成されている GPIO ピンの場合、割り込み要求が割り込みコントローラーではなく GPIO pin によって実装されている、または専用の割り込み要求行がオペレーティングシステムによって完全に抽象化されているという事実。 GPIO 割り込みは、周辺機器ドライバーに抽象割り込みリソースとして提示されます。 これらのリソースの抽象化は、GPIO ドライバースタックとハードウェアアブストラクションレイヤー (HAL) によってサポートされています。 そのため、割り込みリソースを使用する周辺機器ドライバーは、これらのリソースの基礎となる実装に関する詳細をほとんど無視できます。 詳細については、「 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)」を参照してください。

次の図は、2つの周辺機器ドライバーへの GPIO ベースリソースの割り当ての例を示しています。

![gpio ベースのリソースの割り当て例](images/gpioresources.png)

上の図では、次の3つの GPIO ベースのリソースに周辺機器ドライバー A が割り当てられています。

-   2つのデータ入力ピン
-   データ出力ピン
-   割り込み入力ピン

次の2つの GPIO ベースのリソースが、周辺機器ドライバー B に割り当てられています。

-   データ入力ピン
-   割り込み入力ピン

ドライバー A と B は、割り当てられたリソースを[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で受け取ります。 ドライバーが1つまたは複数の GPIO i/o pin のセットをリソースとして受信した場合、ドライバーはこれらのピンへの接続を開いてアクセスすることができます。 ドライバーは WDFIOTARGET ハンドルを取得して接続を識別し、このハンドルに i/o 要求を送信して、これらの pin の読み取りまたは書き込みを行います。

一連の GPIO i/o ピンに接続し、この pin に i/o 要求を送信する方法を示すコード例については、次のトピックを参照してください。

[KMDF ドライバーを GPIO i/o ピンに接続する](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

どちらのトピックでも、コード例の `IoRoutine` 関数は、`ReadOperation` パラメーター値に応じて、読み取りまたは書き込み用の GPIO i/o ピンリソースを開きます。 読み取り用にリソースが開かれている場合 (`DesiredAccess` = 汎用\_読み取り)、リソース内のピンが入力として構成されます。また、pin リソースに送信された[**IOCTL\_GPIO\_read\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)要求では、これらの pin の入力値が読み取られます。 GpioClx では、 [**IOCTL\_gpio\_書き込み\_の pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)要求の書き込みを許可していません。このような要求は、状態\_GPIO\_操作\_拒否されたエラー状態で完了します。 同様に、ピンリソースが書き込み用に開かれている場合 (`DesiredAccess` = 汎用\_書き込み)、リソース内のピンは出力として構成され、 **IOCTL\_GPIO\_書き込み\_** pin 要求は、pin リソースに送信されます。これらのピンを駆動する出力ラッチ。 通常、 **IOCTL\_GPIO\_** を出力ピンセットに読み取り\_pin 要求を送信すると、出力ラッチに書き込まれた最後の値が読み取られます。

割り込みリソースを使用して割り込みを受け取るには、クライアントドライバーは割り込みサービスルーチン (ISR) を割り込みに接続する必要があります。 通常、ドライバーは[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッド (または、場合によっては[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)ルーチン) を呼び出してこの接続を行います。 KMDF 割り込みの詳細については、「 [Interrupt オブジェクトの作成](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-an-interrupt-object)」を参照してください。

ハードウェアプラットフォームとの間で動的に接続および切断できるデバイスとはプラグアンドプレイ対照的に、GPIO コントローラーデバイスは完全に接続されています。 また、GPIO ピンと周辺機器の接続は永続的であると見なされます。 (または、周辺機器がスロットから取り外されている場合、スロットはこのデバイス専用です)。そのため、使用可能な GPIO リソースは固定されており、プラットフォームファームウェアで指定できます。 同様に、GPIO リソースを使用する周辺機器ドライバーは、専用の GPIO リソースセットを使用することを前提としています。 そのため、これらのデバイスドライバーのリソース要件は、プラットフォームファームウェアで指定できます。

プラットフォームファームウェアによって gpio のセットが GPIO i/o リソースとして指定されている場合、ファームウェアは、このリソースのピンを読み取り、書き込み、または読み取りと書き込みの両方に対して開くことができるかどうかを示します。

周辺機器ドライバーで複数の GPIO i/o リソースが使用されている場合、このドライバーは、PnP マネージャーによってこれらのリソースが列挙される順序を認識している必要があります。 たとえば、ドライバーで2つの GPIO i/o ピンが使用されている場合、これらの pin は個別に、または個別にアクセスする必要があるため、プラットフォームファームウェアは各 pin を個別の GPIO i/o リソースとして記述する必要があります。 PnP マネージャーは、これらのリソースをプラットフォームファームウェアで記述されている順序で列挙します。これは、ドライバーが期待する順序と一致している必要があります。

周辺機器ドライバーが GPIO i/o リソースへの接続を開くと、このドライバーがこの接続へのアクセスに送信する\_ピンまたは[**ioctl\_\_gpio**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins) [ **\_読み取りのピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)または ioctl gpio に\_ます。リソース内のすべてのピン。 ドライバーがこれらの pin のサブセットのみにアクセスする必要がある場合は、このサブセットを別のリソースとしてドライバーに割り当てる必要があります。

要求出力バッファーのビットへのデータ入力ピンのマッピングなど、 **ioctl\_GPIO\_読み取り\_** の要求の詳細については、「 [**ioctl\_GPIO\_read\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)」を参照してください。 **Ioctl\_\_gpio**の詳細については、要求入力バッファー内のビットとデータ出力ピンのマッピングなど、\_の要求を書き込みます。また、「 [**ioctl\_GPIO\_書き込み\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)」を参照してください。

 

 





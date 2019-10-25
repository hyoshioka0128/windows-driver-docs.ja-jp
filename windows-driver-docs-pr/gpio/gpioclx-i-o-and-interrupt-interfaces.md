---
title: GpioClx I/O と割り込みインターフェイス
description: 通常、GPIO コントローラーのクライアントは、GPIO ピンに接続される周辺機器のドライバーです。
ms.assetid: F75E9B21-9DA4-4DD9-BB44-59E19EDFC099
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 501a177a544e1158b7b854a1f6475d759248843b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824951"
---
# <a name="gpioclx-io-and-interrupt-interfaces"></a>GpioClx I/O と割り込みインターフェイス


通常、GPIO コントローラーのクライアントは、GPIO ピンに接続される周辺機器のドライバーです。 これらのドライバーでは、低帯域幅のデータ チャネル、デバイス選択の出力、および割り込み要求の入力として GPIO ピンが使用されます。 周辺機器のドライバーにより、データ入力またはデータ出力として構成されている GPIO ピンへの論理接続が開かれます。 これらの接続を使用して、これらのピンに I/O 要求が送信されます。 さらに、周辺機器のドライバーでは、割り込み要求の入力として構成されている GPIO ピンに、割り込みサービス ルーチンを論理的に接続できます。

GPIO ピンは、システムで管理されているハードウェアリソースです。 周辺機器ドライバがデバイスを起動する前に、プラグアンドプレイ (PnP) マネージャがこのドライバにハードウェアリソースの一覧を割り当てます。 このハードウェアリソースの一覧には、次のものが含まれる場合があります。

-   GPIO i/o リソース。 このリソースは、データ入力またはデータ出力として構成される1つ以上の GPIO ピンのセットです。 GPIO i/o リソースは、Windows 8 以降の新しい Windows リソースの種類です。
-   割り込み。 この割り込みリソースは、割り込み入力として構成されている GPIO pin として実装される場合がありますが、プログラミング可能な割り込みコントローラーまたはプロセッサパッケージの専用割り込みピンとして実装される可能性があります。 ハードウェアアブストラクションレイヤー (HAL) の割り込み抽象化は、これらの実装の詳細を非表示にします。クライアントドライバーは無視しても問題ありません。

周辺機器ドライバーがデータ入力または出力として GPIO pin のセットを使用できるようにするには、ドライバーがこれらの pin への論理接続を開く必要があります。 たとえば、[カーネルモードドライバーインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) ドライバーは、WDFIOTARGET ハンドルを取得して接続を識別します。 ドライバーは、このハンドルを使用して、i/o 要求をピンに送信します。 具体的には、クライアントドライバーは、出力ピンにデータを書き込んで入力ピンからデータを読み取るために、\_のピンおよび[**ioctl\_\_gpio**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)に[**書き込みの\_\_gpio**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)に送信します。 一連の GPIO i/o ピンに接続する方法を示すコード例については、次のトピックを参照してください。

[KMDF ドライバーを GPIO i/o ピンに接続する](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

割り込みリソースを使用して割り込みを受け取るには、周辺機器ドライバーが割り込みサービスルーチン (ISR) を割り込みに論理的に接続する必要があります。 たとえば、カーネルモードドライバーは、 [**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドまたは[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)ルーチンを呼び出すことによって、この接続を確立できます。 接続されると、ドライバーの ISR は、周辺機器が GPIO pin または割り込みコントローラー入力に割り込み要求を通知するときに実行されます。 割り込みの詳細については、「 [Interrupt オブジェクトの作成](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-an-interrupt-object)」を参照してください。

GPIO framework 拡張機能 (GpioClx) は、クライアントである周辺機器ドライバーの i/o 接続と割り込み接続の両方を管理します。 PnP マネージャーでは、GPIO コントローラーデバイス上の GPIO ピンの異なるグループを異なるクライアントドライバーに割り当てることがあります。 これらの pin の一部はデータ入力または出力として構成され、一部は割り込み要求入力として構成されます。

クライアントドライバーが割り込み要求を受け取ったり、GPIO ピンに i/o 要求を送信したりすると、GpioClx は、GPIO コントローラードライバーによって実装されたイベントコールバック関数を呼び出します。 これらのコールバックは、GPIO コントローラーデバイス内のハードウェアレジスタにアクセスします。 これらの関数呼び出しを通じて、GpioClx はデータ入力を読み取り、データ出力に書き込み、割り込み要求を管理します (割り込み入力として構成されたクエリ、有効化、マスキング、クリアなど)。

GpioClx は、クライアントによって開かれている i/o と割り込み接続を管理するために必要なすべての処理を実行します。 このような接続の管理を GpioClx に委任することによって、GPIO コントローラードライバーは、GPIO コントローラーデバイス内のハードウェアレジスタにアクセスする比較的単純なタスクのみを担当します。 GPIO controller ドライバーは、特定のアクセスが行われるクライアントドライバーを認識している必要はありません。

 

 





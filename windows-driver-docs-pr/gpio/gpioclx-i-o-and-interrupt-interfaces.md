---
title: GpioClx I/O と割り込みインターフェイス
description: 通常、GPIO コントローラーのクライアントは、GPIO ピンに接続される周辺機器のドライバーです。
ms.assetid: F75E9B21-9DA4-4DD9-BB44-59E19EDFC099
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb94a00384f9b4caf47ecccd3f2c4e023918a337
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363588"
---
# <a name="gpioclx-io-and-interrupt-interfaces"></a>GpioClx I/O と割り込みインターフェイス


通常、GPIO コントローラーのクライアントは、GPIO ピンに接続される周辺機器のドライバーです。 これらのドライバーでは、低帯域幅のデータ チャネル、デバイス選択の出力、および割り込み要求の入力として GPIO ピンが使用されます。 周辺機器のドライバーにより、データ入力またはデータ出力として構成されている GPIO ピンへの論理接続が開かれます。 これらの接続を使用して、これらのピンに I/O 要求が送信されます。 さらに、周辺機器のドライバーでは、割り込み要求の入力として構成されている GPIO ピンに、割り込みサービス ルーチンを論理的に接続できます。

GPIO ピンは、ハードウェアのシステムで管理されるリソースです。 周辺機器のデバイス ドライバーは、そのデバイスを起動する前に、プラグ アンド プレイ (PnP) マネージャーはハードウェア リソースのリストをこのドライバーに割り当てます。 このハードウェア リソースの一覧には、次が含まれます。

-   GPIO I/O リソースです。 このリソースは、一連の 1 つまたは複数の GPIO ピンを入力またはデータのデータの出力として構成されます。 GPIO I/O リソースとは、Windows 8 以降では新しい Windows リソースの種類です。
-   割り込みです。 この割り込みリソースは、割り込みの入力として構成されている GPIO ピンとして実装する場合がありますが、プログラム可能割り込みコント ローラーで、またはプロセッサ パッケージで専用の割り込み pin として代わりに実装する場合があります。 ハードウェア アブストラクション レイヤー (HAL) の割り込みの抽象化には、これらの実装の詳細、どのクライアント ドライバーは無視してかまいませんが非表示にします。

周辺機器のデバイス ドライバーは、GPIO ピンのセットを使用して、データ入力または出力として、前に、ドライバーは、これらのピンへの論理接続を開く必要があります。 たとえば、[カーネル モード ドライバー インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF) ドライバーは接続を識別する WDFIOTARGET ハンドルを取得します。 ドライバーでは、このハンドルを使用して、ピンが I/O 要求を送信します。 具体的には、クライアント ドライバーの送信[ **IOCTL\_GPIO\_書き込み\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)と[ **IOCTL\_GPIO\_読み取り\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins) I/O に対する制御要求の出力ピンにデータを書き込むし、入力ピンからデータを読み取ります。 I/O の GPIO ピンに接続する方法を示すコード例では、次のトピックを参照してください。

[KMDF ドライバーを GPIO I/O ピンに接続します。](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

割り込みリソースを使用すると、割り込みの受信、周辺機器のデバイス ドライバーは割り込みサービス ルーチン (ISR) を割り込みに論理的に接続する必要があります。 カーネル モード ドライバーが呼び出すことによってこの接続を確立するなど、 [ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドまたは[ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)ルーチン。 接続した後は、ドライバーの ISR は周辺機器、GPIO ピンまたは割り込みコント ローラーの入力に割り込み要求を通知するときに実行されます。 割り込みの詳細については、次を参照してください。 [Interrupt オブジェクトを作成する](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-an-interrupt-object)します。

GPIO フレームワーク拡張機能 (GpioClx) は、I/O の接続と周辺機器のデバイス ドライバーはそのクライアントの割り込みの接続の両方を管理します。 PnP マネージャーでは、さまざまなクライアント ドライバーに GPIO ピン GPIO コント ローラー デバイス上の別のグループを割り当てることができます。 これらのピンの一部はデータ入力または出力として構成され、割り込み要求の入力として構成されているいくつか。

ときにクライアント ドライバーは、割り込み要求を受信または GPIO ピン GPIO コント ローラーのドライバーによって実装される GpioClx 呼び出しイベント コールバック関数に I/O 要求を送信します。 これらのコールバックは、GPIO コント ローラー デバイスのハードウェア レジスタにアクセスします。 これらの関数呼び出しによっては、GpioClx はデータ入力を読み取り、データ、出力に書き込み、(でクエリを実行する、有効にすると、マスク、消去、割り込みの入力として構成されている GPIO ピン) 割り込み要求を管理します。

GpioClx では、I/O を管理し、クライアントによって開かれた接続を中断するために必要であるすべての処理を実行します。 GPIO コント ローラーのドライバー-GpioClx これらの接続の管理を委任することで、GPIO コント ローラー デバイスのハードウェア レジスタへのアクセスの比較的単純なタスクのみを担当します。 GPIO コント ローラーのドライバーは、特定のアクセスが行われたクライアント ドライバーを把握する必要はありません。

 

 





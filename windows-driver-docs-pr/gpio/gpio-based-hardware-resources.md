---
title: GPIO ベースのハードウェア リソース
description: Windows 8 以降では、GPIO コントローラーのドライバーによって制御される汎用 I/O (GPIO) ピンは、システムで管理されるハードウェア リソースとして他のドライバーで使用できます。
ms.assetid: 03A6ACDF-8BB7-40C0-A331-7F61F48A44DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8719a9e327495962682b592b8d13e813394b07c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363638"
---
# <a name="gpio-based-hardware-resources"></a>GPIO ベースのハードウェア リソース


Windows 8 以降では、GPIO コントローラーのドライバーによって制御される汎用 I/O (GPIO) ピンは、システムで管理されるハードウェア リソースとして他のドライバーで使用できます。 データ入力またはデータ出力として構成されているピンである GPIO I/O ピンは、新しい種類の Windows リソースである *GPIO I/O リソース*として使用できます。 さらに、割り込み要求の入力として構成されているピンである GPIO 割り込みピンは、通常の Windows 割り込みリソースとして使用できます。

GPIO I/O リソースは、周辺機器のデバイスのドライバーがからの読み取りや書き込みを 1 つまたは複数の GPIO ピンのセットを表します。 Windows では、周辺機器のデバイス ドライバーは抽象の GPIO I/O リソースの操作に書き込むことができるように I/O の GPIO ピンの基になる実装の詳細についてを非表示にします。 これらの抽象リソースを使用して、周辺機器のデバイス ドライバーは、リソースを実装する GPIO コント ローラーのハードウェアに関係なく、プラットフォーム間で操作できます。 GPIO I/O リソースの表現を基になる GPIO ピン留めまたはピンを所有している特定の GPIO コント ローラーのドライバーを使用したこのリソースを関連付ける WDFIOTARGET ハンドルでします。

通常、入力または出力では、コント ローラー ハードウェアとピンに物理的に接続されているデバイスの機能によっては、GPIO コント ローラーで、I/O の pin を構成できます。 そのため、ドライバーは、書き込みまたは読み取り操作は、のいずれかがこのピンへの論理接続を開くことができます。 ただし、ハードウェア、および GPIO フレームワーク拡張機能 (GpioClx) ではなく、この制約が適用されます。 ハードウェアは、I/O をピン留めする入力と出力の両方に構成するのには可能 GpioClx に対して読み取り、暗証番号 (pin) への論理接続を開く操作と書き込み操作するためのドライバーを有効になります。

GPIO ピンが割り込み要求入力、割り込み要求、割り込みコント ローラーでの代わりに GPIO ピンによって実装または専用の割り込み要求行が、オペレーティング システムによって完全に抽象化をファクトとして構成されています。 GPIO 割り込みは、周辺機器のデバイス ドライバーを抽象割り込みリソースとして表示されます。 GPIO ドライバー スタックとハードウェア アブストラクション レイヤー (HAL) は、これらのリソースの抽象化がサポートされています。 したがって、割り込みのリソースを使用して、周辺機器のデバイス ドライバーは、これらのリソースの基になる実装の詳細についてをほとんど無視できます。 詳細については、次を参照してください。 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)します。

次の図は、GPIO ベースのリソースが 2 つの周辺機器のデバイス ドライバーへの割り当ての例を示しています。

![gpio ベースのリソースの例の割り当て](images/gpioresources.png)

A: の周辺機器のデバイス ドライバーが次の 3 つの GPIO ベース リソース上の図では、割り当てられています。

-   2 つのデータ入力ピン
-   データの出力ピン
-   割り込みの入力ピン

周辺機器のデバイス ドライバーの b: 割り当てられている次の 2 つの GPIO ベース リソース

-   データの入力ピン
-   割り込みの入力ピン

A と B のドライバーで、割り当てられたリソースが表示される、 [ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数。 ドライバーが受信した場合、リソースとして 1 つまたは複数の I/O の GPIO ピンのセット、ドライバーは、それらにアクセスするこれらのピンへの接続を開くことができます。 ドライバーは、接続を識別する WDFIOTARGET ハンドルを取得し、I/O 要求から読み取りまたは書き込みをこれらのピンには、このハンドルを送信します。

I/O の GPIO ピンに接続し、この I/O 要求を送信する方法を示すコード例を pin では、次のトピックを参照してください。

[KMDF ドライバーを GPIO I/O ピンに接続します。](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

2 つのトピックで、`IoRoutine`関数のコード例では、読み取りまたは書き込みでは、いずれかに GPIO I/O 暗証番号 (pin) リソースを開くかによって、`ReadOperation`パラメーターの値。 リソースが読み取り用に開かれている場合 (`DesiredAccess` = ジェネリック\_読み取り)、リソース内のピンが、入力として構成されていると、 [ **IOCTL\_GPIO\_読み取り\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins)暗証番号 (pin) のリソースに送信される要求は、これらのピンに入力値を読み取ります。 GpioClx ことはできません、 [ **IOCTL\_GPIO\_書き込み\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)一連の入力ピンに送信される要求し、状態が、このような要求が完了すると\_GPIO\_操作\_拒否エラーの状態。 同様に、暗証番号 (pin) のリソースが書き込み用に開かれている場合 (`DesiredAccess` = ジェネリック\_書き込み)、リソース内のピンは、出力として構成されている**IOCTL\_GPIO\_書き込み\_ピン**暗証番号 (pin) のリソースに送信される要求は、これらのピンを駆動する出力のラッチの値を設定します。 通常、送信、 **IOCTL\_GPIO\_読み取り\_ピン**要求の出力ピンを出力ラッチに書き込まれた最後の値を読み取るだけです。

割り込みリソースを使用すると、割り込みを受信して、クライアント ドライバーは、割り込みに割り込みサービス ルーチン (ISR) を接続する必要があります。 通常、この接続は呼び出すことによって、ドライバー、 [ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッド (または場合によって、 [ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)ルーチン)。 KMDF 割り込みの詳細については、次を参照してください。 [Interrupt オブジェクトを作成する](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-an-interrupt-object)します。

プラグ アンド プレイ デバイスを動的に接続されているし、ハードウェア プラットフォームから切断されていることができますとは対照的 GPIO コント ローラーのデバイスは完全にアタッチされます。 また、GPIO ピンと周辺機器のデバイス間の接続が永続的と見なされます。 (または、スロットがこのデバイスに専用のスロットから、周辺機器が接続されていることができますが場合、)。そのため、使用可能な GPIO リソースは固定されており、プラットフォーム ファームウェアで指定できます。 同様に、GPIO リソースを使用して、周辺機器のデバイス ドライバーは、GPIO リソースの専用のセットを使用すると見なされます。 したがって、これらのデバイス ドライバーのリソース要件は、プラットフォーム ファームウェアで指定できます。

指定した場合、プラットフォーム ファームウェアの GPIO ピン GPIO I/O リソースとして、ファームウェアは、読み取り、書き込み、または読み取りと書き込みの両方に対して、このリソースのピンを開くことができるかどうかを示します。

周辺機器のデバイス ドライバーは、1 つ以上の GPIO I/O リソースを使用している場合このドライバーは PnP マネージャーによってこれらのリソースを列挙する注文の対応である必要があります。 たとえば、ドライバーは、2 つの I/O の GPIO ピンを使用して、個別に、別々 の時期に、これらのピンをアクセスする必要があります、プラットフォーム ファームウェアする必要があります各ピン GPIO I/O の別個のリソースとして説明します。 PnP マネージャーでは、プラットフォームのファームウェアは、ドライバーで想定される順序に一致する必要がありますで説明した順序でこれらのリソースを列挙します。

周辺機器のデバイス ドライバーは、GPIO I/O リソースへの接続を開いた後、 [ **IOCTL\_GPIO\_読み取り\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins)または[ **IOCTL\_GPIO\_書き込み\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)このドライバーは、この接続に送信する要求はすべてのリソースのピンにアクセスします。 ドライバーでは、これらのピンのサブセットのみをアクセスする必要がある場合がある場合、このサブセットを個別のリソースがドライバーに割り当てる必要があります。

詳細については**IOCTL\_GPIO\_読み取り\_ピン**、要求の出力バッファーにデータ入力ピンが、bits のマッピングを含む要求を参照してください[ **IOCTL\_GPIO\_読み取り\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins)します。 詳細については**IOCTL\_GPIO\_書き込み\_ピン**データの出力ピンに要求の入力バッファー内のビットのマッピングを含む要求を参照してください[ **IOCTL\_GPIO\_書き込み\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)します。

 

 





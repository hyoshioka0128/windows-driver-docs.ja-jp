---
title: SerCx2 で管理されるシリアル ポート上のデバイスの周辺機器ドライバー
description: 通常、SerCx2 によって管理されるシリアルポートは、周辺機器に永続的に接続されます。
ms.assetid: 06412F66-3192-4D25-BDBA-FAB2211519DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 255ccc3272eb13935b38e0d5342b7c75d0c11b1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844946"
---
# <a name="peripheral-drivers-for-devices-on-sercx2-managed-serial-ports"></a>SerCx2 で管理されるシリアル ポート上のデバイスの周辺機器ドライバー

通常、SerCx2 によって管理されるシリアルポートは、周辺機器に永続的に接続されます。 このデバイスは、シリアルポートに i/o 要求を送信する周辺機器ドライバーによって制御されます。 これらの要求は、デバイスとの間でデータを転送し、シリアルポートの状態を構成します。 周辺ドライバーによって送信された i/o 要求は、SerCx2 と関連付けられているシリアルコントローラードライバーによって共同処理されます。

多くの場合、serial controller はチップ (SoC) の統合回線上のシステムに含まれています。 SoC チップのシリアルコントローラーのシリアルポートに接続されている周辺機器の例としては、GPS、ワイヤレス LAN、カメラ、Bluetooth デバイスなどがあります。

シリアル接続された周辺機器の周辺機器は、通常、[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) または[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) ドライバーです。 このデバイスと通信するには、まず、周辺機器ドライバーがシリアルコントローラーへの論理接続を開き、ドライバーが i/o 要求を送信できるファイルハンドルを受信する必要があります。 詳細については、「 [SerCx2 シリアルポートを開く](opening-a-sercx2-managed-serial-port.md)」を参照してください。

**このページのもの**

- [シリアルドライバーのアーキテクチャ](#serial-driver-architecture)
- [I/o 要求パス](#i-o-request-path)
- [割り込みパス](#interrupt-path)

## <a name="serial-driver-architecture"></a>シリアルドライバーのアーキテクチャ

次のブロック図は、周辺機器 (図の一番下) と、このデバイスの周辺機器 (図の一番上) との間の通信パスを形成するソフトウェアとハードウェアのレイヤーを示しています。 この例では、周辺機器がシリアルコントローラーのポートと、GPIO コントローラーの割り込みピンに接続されています。

![sercx2 で管理されているシリアルポートの周辺機器のソフトウェアとハードウェアのレイヤー](images/seriallayers.png)

この例の周辺機器ドライバーは、周辺機器に i/o 要求を送信する UMDF ドライバーです。 これらの要求は、図の左側に示されている通信パスを経由して移動します。 要求は、SerCx2 とシリアルコントローラードライバーによって処理されます。 周辺ドライバーは、シリアルポートのハードウェア構成 (たとえば、ボーレートを変更する) を設定する i/o 操作を要求したり、シリアルポートを介して周辺機器との間でデータを転送したりすることができます。 詳細については、「 [i/o 要求パス](#i-o-request-path)」を参照してください。

周辺機器からの割り込みは、前の図の右側にある通信パスを上に移動します。 この図の右下隅に示されているように、周辺機器の割り込みピンは、汎用 i/o (GPIO) コントローラーのピンに接続されています。 この GPIO pin は、周辺機器から割り込み信号を受信するように構成されています。 SoC コントローラーは、SoC ベースのハードウェアプラットフォームで、プログラミング可能な割り込みコントローラーの役割を頻繁に果たします。 詳細については、「 [Interrupt path](#interrupt-path)」を参照してください。

図に灰色表示されている2つのブロックは、システム指定のモジュールです。 GPIO framework 拡張機能 (GpioClx) は、Windows 8 以降で使用できます。 SerCx2 と同様、GpioClx は KMDF の拡張機能です。 GpioClx では、さまざまな GPIO コントローラーに共通の機能が実行されます。 GpioClx は、GPIO コントローラーのすべてのハードウェア固有の操作を管理する GPIO コントローラードライバーと連携して動作します。 詳細については、「 [GPIO ドライバーのサポートの概要](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)」を参照してください。

## <a name="i-o-request-path"></a>I O 要求パス

周辺機器にデータを送信するために、周辺機器ドライバーは書き込み ([**IRP\_MJ\_write**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) 要求をシリアルコントローラーに送信します。 周辺機器からデータを受信するために、周辺ドライバーは読み取り ([**IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))) 要求をシリアルコントローラーに送信します。

さらに、Windows は、周辺機器ドライバーがシリアルコントローラーに固有のさまざまな i/o 制御操作を実行するために使用できるデバイス i/o 制御要求 (Ioctl) のセットを定義します。 周辺ドライバーが要求できる i/o 制御操作の例を次に示します。

- シリアルポートがデータの送受信に使用するボーレートを設定します。
- 読み取り要求と書き込み要求のタイムアウト間隔を設定します。
- 周辺ドライバーが通知を受信するシリアルポートで、ハードウェアイベントのセットを指定します。

SerCx2 は、serial framework extension (SerCx) の受信トレイシリアルドライバー、シリアル .sys、バージョン1と同じシリアル Ioctl の多くをサポートしています。 詳しくは、次のトピックをご覧ください。

- SerCx2 が特定のシリアル IOCTL をサポートするかどうかを判断するには、「[直列 I/o 要求インターフェイス](serial-i-o-request-interface.md)」の表を参照してください。
- Windows のシリアル i/o 要求インターフェイスで定義されているすべてのシリアル Ioctl の詳細な説明については、「[シリアルデバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。
- Serial .sys、SerCx、SerCx2 の簡単な概要については、「[シリアルコントローラードライバーの概要](serial-drivers-overview.md)」を参照してください。

## <a name="interrupt-path"></a>割り込みパス

[シリアルドライバーのアーキテクチャ](#serial-driver-architecture)図に示されているように、周辺機器は GPIO pin を使用してデバイスの割り込みを周辺機器ドライバーに送信します。 周辺機器からの割り込み信号に応答して、GPIO コントローラーはプロセッサに対してハードウェア割り込み (*プライマリ*割り込みと呼ばれます) を通知します。 オペレーティングシステムは、この割り込みを GpioClx の ISR に送信します。 次に、GpioClx は、割り込みの原因となった GPIO pin を識別し、周辺機器から仮想割り込み ( *2 次*割り込み) のグローバルシステム割り込み (gsi) 識別子を検索します。 GpioClx によって GSI が HAL に提供され、HAL は周辺ドライバーの ISR を呼び出します。 通常、この割り込みを処理するには、周辺機器ドライバーが SerCx2 とシリアルコントローラードライバーを介して、周辺機器に1つ以上の i/o 要求を送信します。 プライマリとセカンダリの割り込みの詳細については、「 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)」を参照してください。

GPIO 割り込みは、周辺機器でハードウェアイベントの通知を受信するための1つの方法にすぎません。 もう1つの方法は、周辺ドライバーがシリアルポートで特定の種類のハードウェアイベントが発生したときに、SerCx2 とシリアルコントローラードライバーからの通知を要求することです。 たとえば、周辺機器ドライバーは、シリアルコントローラーが周辺機器からシリアルデータを受信したときに通知を受け取るように要求できます。 これらの通知を要求するために、周辺機器ドライバーは、周辺機器への[**待機\_マスク要求\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)して、監視する一連のイベントを指定し、 [**ioctl\_直列を送信する ioctl\_シリアルに送信し\_待機\_\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_wait_on_mask)の要求で、これらのイベントのリッスンを開始します。 これらの要求は、シリアルコントローラードライバーのヘルプを使用して、SerCx2 によって処理されます。 周辺機器ドライバーが監視できるイベントの種類の詳細については、「 **serial\_EV\_* XXX***」を参照してください。これは、 [**IOCTL\_serial\_SET\_WAIT\_MASK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)に記述されています。

ただし、シリアルコントローラーは、D0 デバイスの電源状態にある場合にのみ、ハードウェアイベントを検出できます。 シリアルコントローラーが低電力状態の場合、周辺機器は、たとえば、周辺機器にドライバーの新しいデータがあることを確認するために、シリアルコントローラーからの通知に依存することはできません。 この場合、周辺機器は、GPIO pin を使用して割り込み信号 (または、場合によってはウェイク信号) を送信する必要があります。 GPIO コントローラーの電力消費はほとんどなく、通常は他の多くのデバイスが低電力状態になった後もアクティブなままになります。

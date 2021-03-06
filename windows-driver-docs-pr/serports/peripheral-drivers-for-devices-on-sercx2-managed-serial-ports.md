---
title: SerCx2 で管理されるシリアル ポート上のデバイスの周辺機器ドライバー
description: 通常、SerCx2 によって管理されているシリアル ポートは周辺機器に接続されている永続的にします。
ms.assetid: 06412F66-3192-4D25-BDBA-FAB2211519DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0efd8e2e85ee7029d8f0e368d427575ddd126298
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386944"
---
# <a name="peripheral-drivers-for-devices-on-sercx2-managed-serial-ports"></a>SerCx2 で管理されるシリアル ポート上のデバイスの周辺機器ドライバー

通常、SerCx2 によって管理されているシリアル ポートは周辺機器に接続されている永続的にします。 このデバイスは、シリアル ポートへの I/O 要求を送信する周辺ドライバーによって制御されます。 これらの要求は、デバイスとデータの転送し、シリアル ポートの状態を構成します。 周辺機器のドライバーによって送信された I/O 要求は、SerCx2 と関連付けられているシリアル コント ローラー ドライバーによって共同で処理されます。

多くの場合、シリアル コント ローラーは、チップ (SoC) 統合の回線でシステムに格納されます。 SoC オンチップ シリアル コント ローラーのシリアル ポートに接続されている周辺機器の例には、GPS、ワイヤレス LAN、カメラ、および Bluetooth デバイスが含まれます。

周辺機器のドライバーを逐次的に接続されている周辺機器は、通常、[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF) または[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) ドライバー。 このデバイスを通信するには、周辺機器のドライバーが最初シリアル コント ローラーへの論理接続を開くし、ドライバーが I/O 要求を送信するファイル ハンドルが表示される必要があります。 詳細については、次を参照してください。 [SerCx2-Managed シリアル ポートを開く](opening-a-sercx2-managed-serial-port.md)します。

**このページで**

- [シリアル ドライバーのアーキテクチャ](#serial-driver-architecture)
- [I/O 要求のパス](#i-o-request-path)
- [パスを中断します。](#interrupt-path)

## <a name="serial-driver-architecture"></a>シリアル ドライバーのアーキテクチャ

(図の下部) の周辺機器とこのデバイスの周辺機器のドライバー (図の上部) の間の通信パスを形成するソフトウェアとハードウェアのレイヤーを次のブロック図に示します。 この例では、シリアル コント ローラーのポートと、割り込みピン GPIO コント ローラー上に周辺機器が接続されています。

![sercx2 で管理されたシリアル ポート上の周辺機器デバイス用のソフトウェアとハードウェアのレイヤー](images/seriallayers.png)

この例では、周辺機器のドライバーは、周辺機器への I/O 要求を送信する UMDF ドライバーです。 これらの要求は、図の左側に表示される通信パスを移動します。 要求は、SerCx2 とシリアル コント ローラー ドライバーによって処理されます。 周辺機器のドライバーは、シリアル ポートのハードウェア構成を設定する I/O 操作を要求できます (たとえば、ボー レート変更) し、シリアル ポート経由の周辺機器とデータを転送します。 詳細については、次を参照してください。 [I/O 要求パス](#i-o-request-path)します。

周辺機器旅行上方向、通信パスを前の図の右側にあるを中断します。 この図の右下に示すように、周辺機器のデバイスからの割り込みのピンは、汎用入出力 (GPIO) コント ローラー上のピンに接続されます。 周辺機器のデバイスからの割り込みシグナルを受信するこの GPIO ピンが構成されます。 SoC ベースのハードウェア プラットフォームでは、GPIO コント ローラーは頻繁にプログラム可能割り込みコント ローラーの役割を果たします。 詳細については、次を参照してください。[割り込みパス](#interrupt-path)します。

灰色の図に示すように 2 つのブロックは、システムが指定したモジュールです。 GPIO フレームワーク拡張機能 (GpioClx) では、Windows 8 以降で使用できます。 SerCx2 などは、GpioClx は KMDF の拡張機能です。 GpioClx は、GPIO コント ローラーのさまざまな共通の関数を実行します。 GpioClx は、GPIO コント ローラーのすべてのハードウェアに固有の操作を管理する GPIO コント ローラーのドライバーで動作します。 詳細については、次を参照してください。 [GPIO ドライバー サポートの概要](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)します。

## <a name="i-o-request-path"></a>要求パスでは、O

周辺機器のドライバーを周辺機器へデータを送信するには、書き込みを送信します ([**IRP\_MJ\_書き込み**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) シリアル コント ローラーに要求します。 周辺機器のドライバーを周辺機器のデバイスからデータを受信するには、読み取りを送信します ([**IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))) シリアル コント ローラーに要求します。

さらに、Windows では、一連の周辺機器のドライバーを使用してシリアル コント ローラーに固有のさまざまな I/O 制御操作を実行するデバイス I/O 制御要求 (Ioctl) を定義します。 周辺機器のドライバーが要求できる I/O 制御操作の例を次に示します。

- シリアル ポートが送信され、データを受信、ボー レートを設定します。
- 読み取りのタイムアウト間隔を設定および書き込み要求。
- シリアル ポート周辺機器のドライバーが通知を受信するハードウェア イベントのセットを指定します。

SerCx2 シリアル ドライバーの受信トレイ、際に、およびシリアル フレームワークの拡張機能 (SerCx) のバージョン 1 と同じシリアル Ioctl の多くをサポートします。 詳しくは、次のトピックをご覧ください。

- 表を参照して[シリアル I/O 要求インターフェイス](serial-i-o-request-interface.md)SerCx2 が特定のシリアル IOCTL をサポートするかどうかを確認します。
- 参照してください[シリアル デバイスに対する制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)Windows シリアル I/O 要求インターフェイスによって定義されているすべてのシリアル Ioctl の詳細についてはします。
- 参照してください[シリアル コント ローラーのドライバーの概要](serial-drivers-overview.md)の際に、SerCx、および SerCx2 を簡単に紹介します。

## <a name="interrupt-path"></a>パスを中断します。

ように、[シリアル ドライバーのアーキテクチャ](#serial-driver-architecture)図では、周辺機器を使用して GPIO ピン留めデバイス割り込みを周辺のドライバーに送信します。 周辺機器のデバイスからの割り込みシグナルに対して、GPIO コント ローラーがハードウェア割り込みを通知 (と呼ばれる、*プライマリ*割り込み) プロセッサにします。 オペレーティング システムに指示する GpioClx の ISR. 割り込み 次に、GpioClx はどの GPIO ピン留めする、割り込みの原因を識別し、仮想の割り込みのグローバル システムの割り込み (GSI) 識別子を検索 (と呼ばれる、*セカンダリ*割り込み) 周辺機器から。 GpioClx 装置、HAL を HAL GSI 呼び出し、周辺機器のドライバーの ISR. 通常周辺のドライバーは、割り込みを処理するために、SerCx2 とシリアル コント ローラーのドライバーを使用して周辺機器に 1 つまたは複数の I/O 要求を送信します。 プライマリとセカンダリの割り込みの詳細については、次を参照してください。 [GPIO 割り込み](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)します。

GPIO 割り込みは、周辺機器のデバイスでハードウェア イベントの通知を受け取る周辺のドライバーの 1 つだけの方法です。 別の方法は、周辺機器のドライバーに通知を要求 SerCx2 とシリアル コント ローラー ドライバーからシリアル ポートで特定の種類のハードウェア イベントが発生した場合です。 たとえば、周辺機器のドライバーは、シリアル コント ローラーは、周辺機器からシリアル データを受け取るときに通知を要求できます。 これらの通知を要求するには、周辺機器のドライバーを送信、 [ **IOCTL\_シリアル\_設定\_待機\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)周辺機器への要求イベントを監視して、送信のセットを指定する、 [ **IOCTL\_シリアル\_待機\_ON\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_wait_on_mask)要求のリッスンを開始これらのイベントです。 これらの要求は、コント ローラーのシリアル ドライバーのサポートで SerCx2、によって処理されます。 周辺機器のドライバーを監視できるイベントの種類の詳細については、次を参照してください**シリアル\_EV\_* XXX*** で説明される[ **IOCTL\_シリアル。\_設定\_待機\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)します。

ただし、シリアル コント ローラーは、ハードウェア イベント D0 デバイスの電源状態にあるときにのみを検出できます。 シリアル コント ローラーが低電力状態にある場合、周辺機器のドライバーは、たとえば、周辺機器のデバイスには新しいデータを読み取るドライバーをする場合に知ってシリアル コント ローラーからの通知を使用できません。 この場合は、周辺機器する必要があります割り込みシグナルを (または送信、ウェイク信号おそらく、) GPIO ピンから。 GPIO コント ローラーがほとんど電力を消費し、通常はアクティブなまま他のほとんどのデバイスが省電力状態を入力した後にします。

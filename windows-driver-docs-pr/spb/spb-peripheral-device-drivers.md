---
title: SPB 周辺機器ドライバー
description: SPB の周辺機器のデバイス ドライバーは、シンプルな周辺機器バス (SPB) に接続されている周辺機器を制御します。
ms.assetid: 8352EBD9-D94C-4EC6-A17E-3A72DDE4C16C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f370d0c736b10365e77cb81fdc087804b8f45b67
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394116"
---
# <a name="spb-peripheral-device-drivers"></a>SPB 周辺機器ドライバー


SPB 周辺機器デバイス ドライバーは、SPB ([simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))) に接続された周辺機器を制御します。 このデバイスのハードウェア レジスターは、SPB を介してのみ利用できます。 デバイスに対して読み取りまたは書き込みを行うには、ドライバーから SPB コントローラーに I/O 要求を送信する必要があります。 このコントローラーのみが、デバイスとの間で SPB を経由したデータ転送を開始できます。

Windows 8 以降、Windows によりドライバーのサポート、周辺機器の[単純な周辺機器のバス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPBs)。 I²C および SPI などの SPBs は加速度計、GPS デバイス、およびバッテリ レベル モニターなどの低速センサー デバイスへの接続に広く使用されます。 この概要では、他のシステム コンポーネントと連携、SPB の周辺機器のデバイス ドライバーが SPB に接続されている周辺機器を制御する方法について説明します。

SPB の周辺機器のデバイス ドライバーを使用するように構築できる、[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) または[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF)。 UMDF ドライバーの開発に関する詳細については、次を参照してください。 [UMDF 入門](https://docs.microsoft.com/previous-versions/ff554928(v=vs.85))します。 KMDF ドライバーの開発に関する詳細については、次を参照してください。[カーネル モード ドライバー フレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)します。

## <a name="device-configuration-information"></a>デバイスの構成情報


Sp B に接続されている周辺機器のハードウェア レジスタは、メモリ マップできません。 デバイスは、SPB のコント ローラーは、逐次的に SPB を介して、デバイス間でデータを転送を介してのみアクセスできます。 I/O 操作を実行する SPB の周辺機器のデバイス ドライバーは、デバイスを I/O 要求を送信し、SPB コント ローラーは、これらの要求を完了するために必要なデータ転送を実行します。 SPBs の周辺機器のデバイスに送信できる I/O 要求の詳細については、次を参照してください。 [SPB I/O 要求インターフェイスを使用して](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-i-o-request-interface)します。

次の図は、ハードウェア構成の例を示します、SPB: この場合、I²C バスで — チップ (SoC) モジュール上のシステムに 2 つの周辺機器を接続します。 周辺機器は、SoC モジュールの外部モジュールの 4 つのピンに接続します。 SoC モジュールには I²C コント ローラーをさらに、メインのプロセッサ (非表示) が含まれています、[汎用 I/O](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview) (GPIO) コント ローラー。 プロセッサは、逐次的に 2 つの周辺機器とデータを送信するのに I²C コント ローラーを使用します。 これらのデバイスからの割り込み要求行は、割り込みの入力として構成されている 2 つの GPIO ピンに接続されます。 デバイス信号を割り込み要求、GPIO コント ローラーは、プロセッサに割り込みを中継します。

![spb の周辺機器の接続](images/spbconnects.png)

SoC モジュールには、GPIO コント ローラーとこの例では I²C コント ローラーが統合されているのでのハードウェア レジスタのメモリ マッピングし、プロセッサに直接アクセスできます。 ただし、プロセッサ アクセスできます 2 つの周辺機器のハードウェア レジスタのみ直接 I²C コント ローラーを経由。

SPB でない、[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)(PnP) バスし、自動的に検出して、バスに接続されている新しいデバイスの構成に使用することはできません。 Sp B に接続されたデバイスの接続バスと割り込み接続は、頻繁に永続的なです。 スロットから、デバイスが接続されていることができますが、場合もこのスロットには、デバイスは専用通常です。 さらに、SPB では、バス コント ローラーに、バス上の周辺機器のデバイスからの割り込み要求をリレーするため、帯域内のハードウェア パスが提供はしません。 代わりに、割り込みのハードウェアのパスは、バス コント ローラーとは別です。

ハードウェア プラットフォーム ベンダーは、プラットフォームの ACPI ファームウェアで SPB に接続されている周辺機器の構成情報を格納します。 システムの起動時に、 [ACPI ドライバー列挙](https://docs.microsoft.com/windows-hardware/drivers/acpi/enumerating-child-devices-and-control-methods)PnP マネージャーは、バス上のデバイス。 列挙された各デバイスには、ACPI は、デバイスのバスと割り込み接続に関する情報を提供します。 PnP マネージャーと呼ばれるデータ ストアにこの情報を格納する、*リソース ハブ*します。

PnP マネージャーが一連のデバイスのドライバーを提供する、デバイスが起動時に[ハードウェア リソース](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)リソース ハブがデバイスに格納している構成情報をカプセル化します。 これらのリソースには、接続の ID と、割り込みの数が含まれます。 接続 ID は、SPB コント ローラー、bus アドレス、およびバス クロック周波数などのバス接続情報をカプセル化します。 I/O 要求は、デバイスに送信されることができます、前に、ドライバーがデバイスへの論理接続を開く接続の ID を使用する必要があります最初。 割り込みの数は、ドライバーがその割り込みサービス ルーチン (ISR) を接続できる Windows 割り込みリソースです。 ドライバー簡単に移植できます 1 つのハードウェア プラットフォームから別の接続の ID と割り込みの数は物理バスと割り込み接続に関するプラットフォーム固有の情報を非表示にする高レベルの抽象化であるためです。

## <a name="software-and-hardware-layers"></a>ソフトウェアとハードウェア レイヤー


次のブロック図は、デバイスを使用するアプリケーション プログラムに、SPB の周辺機器を接続するソフトウェアとハードウェアのレイヤーを示しています。 この例では、SPB の周辺機器のデバイス ドライバーは、UMDF ドライバーです。 (図の下部) の周辺機器は、センサー デバイス (たとえば、加速度計)。 上の図のように周辺機器が I²C バスに接続し、信号がピン GPIO コント ローラー経由で要求を中断します。

![センサーの sp b に接続されたデバイスのソフトウェアとハードウェアのレイヤー](images/spblayers.png)

灰色で表示する 3 つのブロックは、システムが指定したモジュールです。 Windows 7 では、以降では、[センサー クラス拡張](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-the-sensor-class-extension)は、UMDF にセンサー固有の拡張機能として入手できます。 Windows 8 では、以降では、 [SPB フレームワーク拡張](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)(SpbCx) と[GPIO フレームワーク拡張](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)(GpioClx) KMDF SPB のコント ローラーに固有の機能を実行する拡張機能として利用GPIO コント ローラーに、それぞれします。

前の図の上部にあるアプリケーションは、メソッドを呼び出して、[センサー API](https://docs.microsoft.com/windows/desktop/SensorsAPI/portal)または[Location API](https://docs.microsoft.com/windows/desktop/LocationAPI/windows-location-api-portal)センサー デバイスと通信します。 これらの呼び出しを通じてアプリケーションが、デバイスに I/O 要求を送信し、デバイスからイベント通知を受信します。 これらの Api の詳細については、次を参照してください。 [Sensor and Location プラットフォームで Windows の概要](https://docs.microsoft.com/windows-hardware/drivers/sensors/introduction-to-the-sensor-and-location-platform-in-windows)します。

アプリケーション SPB の周辺機器のデバイス ドライバーとの通信を必要とするメソッドを呼び出すとセンサー API または Location API を I/O 要求を作成および SPB の周辺機器のデバイス ドライバーに送信します。 センサー クラスの拡張機能モジュールでは、これらの I/O 要求の処理でドライバーを支援します。 ドライバーは、新しい I/O 要求を受信したときに、ドライバーはすぐにセンサー クラスの拡張ドライバーが処理する準備が整うまで、要求をキューに要求を送ります。 アプリケーションからの I/O 要求は、周辺機器のデバイスからのデータの転送を必要とする場合、SPB の周辺機器のデバイス ドライバーはこの転送の I/O 要求を作成し、I²C コント ローラーに要求を送信します。 このような要求は、SpbCx と I²C コント ローラー ドライバーによって共同で処理されます。

SpbCx には、SPB コント ローラー、この例では、I²C コント ローラーなどの I/O 要求のキューを管理するシステム提供のコンポーネントです。 コント ローラーのハードウェア ベンダーによって提供される、I²C コント ローラー ドライバーでは、I²C コント ローラーのすべてのハードウェアに固有の操作を管理します。 たとえば、コント ローラーのドライバーでは、I²C バス経由でと周辺機器のデバイスからのデータ転送を開始するコント ローラーのメモリ マップト ハードウェア レジスタにアクセスします。

周辺機器のデバイスに通知ハードウェア イベントが発生したときに、割り込み要求、SPB の周辺機器のデバイス ドライバーまたはユーザー モード アプリケーションから注意が必要です。 周辺機器のデバイスからの割り込みの線は、割り込み要求を受信するように構成された GPIO ピンに接続されます。 デバイス信号を GPIO ピンに割り込み、GPIO コント ローラーは、プロセッサに割り込みを通知します。 この割り込みに応答してで、カーネルの割り込みのトラップ ハンドラーを呼び出す GpioClx の ISR. この ISR では、割り込みの GPIO ピンを識別するために GPIO コント ローラーのメモリ マップト ハードウェア レジスタにアクセスし、GPIO コント ローラー ドライバーを照会します。 ミュートする割り込み、GPIO コント ローラーのドライバー (割り込みは、edge によってトリガーされる) 場合をクリアするか、またはマスク (場合レベルによってトリガーされる) GPIO ピンの割り込み要求。 プロセッサがトラップ ハンドラーによって返された同じ割り込みをもう一度実行するを防ぐために、割り込みを消せなかったりする必要があります。 レベル トリガーの割り込み SPB の周辺機器のデバイス ドライバーの ISR GPIO ピンはマスクに解除する前に、割り込みをクリアする周辺機器のデバイスのハードウェア レジスタにアクセスする必要があります。

IRQL で実行する SPB の周辺機器のデバイス ドライバーの ISR スケジュール、カーネルの割り込みのトラップ ハンドラーから制御が戻る前にパッシブ =\_レベル。 Windows 8 以降、UMDF ドライバーに接続できるその ISR; 抽象 Windows 割り込みリソースとしてドライバーを受信する割り込み詳細については、次を参照してください。[割り込み処理](https://docs.microsoft.com/windows-hardware/drivers/wdf/handling-interrupts)します。 呼び出している ISR を確認するのには、オペレーティング システムは、割り込みの GPIO ピンに割り当てられ、割り込みに接続されている ISR を検索する仮想割り込みを検索します。 この仮想割り込みが付いて、*セカンダリ*割り込み上の図。 これに対し、GPIO コント ローラーからハードウェアの割り込みとしてラベル付け、*プライマリ*割り込みです。

パッシブのレベルで実行される SPB の周辺機器のデバイス ドライバーの ISR、ため ISR は周辺機器のデバイスのハードウェア レジスタにアクセスするのに同期 I/O 要求を使用できます。 これらの要求を完了するまで、ISR をブロックできます。 ISR、相対的に高い優先順位で実行されは、できるだけ早くを返すし、すべてのバック グラウンド優先度の低いで実行されているワーカーのルーチンへの割り込みの処理を延期する必要があります。

セカンダリの割り込みに応答してでは、SPB の周辺機器のデバイス ドライバーは、センサー API または Location API を介してイベントのユーザー モード アプリケーションに通知するセンサー クラスの拡張で、イベントを投稿します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-i-o-request-interface" data-raw-source="[Using the SPB I/O Request Interface](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-i-o-request-interface)">SPB の I/O 要求インターフェイスを使用します。</a></p></td>
<td><p>Windows 8 では、以降では、 <a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB framework extension](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)">SPB フレームワーク拡張</a>(SpbCx) がサポートするシステム提供のコンポーネント、 <a href="https://docs.microsoft.com/previous-versions/hh698224(v=vs.85)" data-raw-source="[SPB I/O request interface](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))">SPB の I/O 要求インターフェイス</a>。 SPB 周辺機器のデバイス ドライバーを I²C、SPI、およびその他に接続されているデバイスの I/O 要求を送信するこのインターフェイスを使用して<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral buses](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">単純な周辺機器のバス</a>(SPBs)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices" data-raw-source="[Connection IDs for SPB-Connected Peripheral Devices](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)">Sp B に接続されている周辺機器の接続 Id</a></p></td>
<td><p>ドライバーは、周辺機器の I/O 要求送信する前に、<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">シンプルな周辺機器のバス</a>(SPB) ドライバーは、デバイスへの論理接続を開く必要があります。 この接続を介して、ドライバーは、送信、読み取りと書き込みをして、デバイスからデータを転送する要求。 さらに、ドライバー、I/O コントロール (IOCTL) 要求を送信できます SPB 固有の操作を実行するデバイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spb-device-stacks" data-raw-source="[SPB Device Stacks](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-device-stacks)">SPB デバイス スタック</a></p></td>
<td><p>Windows ドライバー モデル明確に区分ドライバー コンポーネント (たとえば、温度センサーなど) の周辺機器を制御するバスのバスのコント ローラーとの間のデータとコントロールの情報を転送を管理するドライバー コンポーネントから、周辺機器です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/interrupts-from-spb-connected-peripheral-devices" data-raw-source="[Interrupts from SPB-Connected Peripheral Devices](https://docs.microsoft.com/windows-hardware/drivers/spb/interrupts-from-spb-connected-peripheral-devices)">周辺機器の SPB 接続からの割り込み</a></p></td>
<td><p>など、PCI バスとは異なり、<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">シンプルな周辺機器のバス</a>(SPB) など、I²C または SPI、標準化、no を提供します。 バス固有意味周辺機器からすると、プロセッサの割り込み要求を伝達するためにします。 代わりに、SPB に接続された周辺機器は、SPB と SPB コントローラー両方の外側にある別のハードウェア パスを介して割り込みを通知します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers" data-raw-source="[Hardware Resources for Kernel-Mode SPB Peripheral Drivers](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers)">カーネル モード SPB の周辺機器のドライバーのハードウェア リソース</a></p></td>
<td><p>コード例では、このトピックの「表示方法、<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)">カーネル モード ドライバー フレームワーク</a>上周辺機器のデバイス用の (KMDF) ドライバーを<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">シンプルな周辺機器のバス</a>(SPB) ために必要なハードウェア リソースを取得しますデバイスを動作します。 これらのリソースに含まれるは、ドライバーがデバイスへの論理接続を確立するために使用する情報です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers" data-raw-source="[Hardware Resources for User-Mode SPB Peripheral Drivers](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)">ユーザー モード SPB の周辺機器のドライバーのハードウェア リソース</a></p></td>
<td><p>コード例では、このトピックの「表示方法、<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf" data-raw-source="[User-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)">ユーザー モード ドライバー フレームワーク</a>上周辺機器のデバイス用の (UMDF) ドライバー、<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">シンプルな周辺機器のバス</a>(SPB) が動作するために必要なハードウェア リソースを取得しますデバイスです。 これらのリソースに含まれるは、ドライバーがデバイスへの論理接続を確立するために使用する情報です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/full-duplex-i-o-requests" data-raw-source="[Full-Duplex I/O Requests](https://docs.microsoft.com/windows-hardware/drivers/spb/full-duplex-i-o-requests)">全二重 I/O 要求</a></p></td>
<td><p>SPI などのいくつかのバスは、全二重バスの転送をサポートします。 これらの転送では、同時にデータをデバイスに書き込むと、同じデバイスからデータを読み取るで I/O のパフォーマンスが向上します。 全二重バスの転送をサポートするために、<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">シンプルな周辺機器のバス</a>(SPB) <a href="https://docs.microsoft.com/previous-versions/hh698224(v=vs.85)" data-raw-source="[I/O request interface](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))">I/O 要求インターフェイス</a>定義、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh974774" data-raw-source="[&lt;strong&gt;IOCTL_SPB_FULL_DUPLEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh974774)"> <strong>IOCTL_SPB_FULL_DUPLEX</strong> </a>I/O 制御コード (IOCTL)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/atomic-bus-operations" data-raw-source="[Atomic Bus Operations](https://docs.microsoft.com/windows-hardware/drivers/spb/atomic-bus-operations)">アトミック Bus の操作</a></p></td>
<td><p>Sp B に接続されている周辺機器の特定のハードウェア機能を使用するには、SPB コント ローラー (つまり、周辺ドライバー) のクライアントは、バスのアトミック操作として、デバイスとのデータ転送のシーケンスを実行する必要があります。 転送シーケンスは、他のクライアント データを転送できますなしに、またはデバイスからバス上、シーケンスが終了するまでためアトミックです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spb-connection-locks" data-raw-source="[SPB Connection Locks](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-connection-locks)">SPB 接続ロック</a></p></td>
<td><p>接続のロックはでターゲットの周辺機器へのアクセスを共有する 2 つのクライアントを有効にするために便利です、<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">シンプルな周辺機器のバス</a>(SPB)。 両方のクライアントは、同じターゲット デバイスへの論理接続を開き、いずれかのクライアントは、一連の I/O 操作を実行するデバイスへの排他アクセスを必要とする場合、接続のロックを使用できます。 1 つのクライアントは、接続のロックを保持しているときに、最初のクライアントは、ロックを解放するまで、デバイスにアクセスする 2 つ目のクライアントによって要求が自動的に保留します。</p></td>
</tr>
</tbody>
</table>

 

 

 





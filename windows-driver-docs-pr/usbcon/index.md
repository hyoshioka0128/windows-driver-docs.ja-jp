---
Description: ユニバーサル シリアル バス (USB) は、ホットプラグ対応で拡張性のあるプラグ アンド プレイ シリアル インターフェイスを提供します。このインターフェイスによって、キーボード、マウス、ジョイスティック、プリンター、スキャナー、記憶装置、モデム、ビデオ会議用カメラなどの周辺機器を低コストの標準方式で接続できます。 PS/2、シリアル ポート、パラレル ポートなど、旧式ポートを使用する周辺機器については、すべて USB に移行することをお勧めします。 USB-IF は Special Interest Group (SIG) であり、公式の USB 仕様、テスト仕様、テスト ツールを保守しています。 Windows オペレーティング システムは、公式の USB 仕様に準拠する USB ホスト コントローラー、ハブ、デバイス、システムをネイティブ サポートしています。 Windows からはプログラミング インターフェイスも提供されます。これを使用し、USB デバイスと通信するデバイス ドライバーやアプリケーションを開発できます。
title: ユニバーサル シリアル バス (USB)
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 00f9dbd93e7ee1bd11c1c6d20c9cba097f9ee903
ms.sourcegitcommit: 4c67665bf7cd4fd3599ff0751a3b0427d119937c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2019
ms.locfileid: "59554066"
---
# <a name="universal-serial-bus-usb"></a>ユニバーサル シリアル バス (USB)


ユニバーサル シリアル バス (USB) は、ホットプラグ対応で拡張性のあるプラグ アンド プレイ シリアル インターフェイスを提供します。このインターフェイスによって、キーボード、マウス、ジョイスティック、プリンター、スキャナー、記憶装置、モデム、ビデオ会議用カメラなどの周辺機器を低コストの標準方式で接続できます。 PS/2、シリアル ポート、パラレル ポートなど、旧式ポートを使用する周辺機器については、すべて USB に移行することをお勧めします。

USB-IF は Special Interest Groups (SIGs) であり、[公式の USB 仕様](http://www.usb.org/developers/docs/)、テスト仕様、テスト ツールに準拠しています。

Windows オペレーティング システムは、公式の USB 仕様に準拠する USB ホスト コントローラー、ハブ、デバイス、システムをネイティブ サポートしています。 Windows からはプログラミング インターフェイスも提供されます。これを利用し、USB デバイスと通信する[デバイス ドライバー](usb-driver-development-guide.md)や[アプリケーション](developing-windows-applications-that-communicate-with-a-usb-device.md)を開発できます。

[![デバイス ビルダーのための USB](images/icon-dev.png)](building-usb-devices-for-windows.md)[![ドライバー開発者のための USB](images/icon-driver.png)](usb-driver-development-guide.md)[![アプリ開発者のための USB](images/icon-app.png)](developing-windows-applications-that-communicate-with-a-usb-device.md)[![USB HCK 証明](images/icon-cert.png)](windows-hardware-certification-kit-tests-for-usb.md)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Windows の USB</strong>
<p></p>
<a href="windows-10--what-s-new-for-usb.md" data-raw-source="[Windows 10: What's new for USB](windows-10--what-s-new-for-usb.md)">Windows 10:USB の新機能</a>
<p>Windows 10 の USB 関連の新機能と機能強化の概要。</p>
<a href="usb-faq--introductory-level.md" data-raw-source="[USB FAQ](usb-faq--introductory-level.md)">USB に関する FAQ</a>
<p>USB スタックと USB でサポートされている機能についてドライバー開発者からよく寄せられている質問。</p>
<a href="microsoft-defined-usb-descriptors.md" data-raw-source="[Microsoft OS Descriptors for USB Devices](microsoft-defined-usb-descriptors.md)">USB デバイスのための Microsoft OS 記述子</a>
<p>Windows では、Windows オペレーティング システムを実行しているシステムに接続されているときに列挙機能を改善する MS OS 記述子が定義されています</p>
<strong>Microsoft が提供する USB ドライバー</strong>
<p></p>
<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows の USB デバイス側ドライバー</a>
<p>USB デバイスの共通関数ロジックを処理するためのドライバー セット。</p>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows の USB ホスト側ドライバー</a>
<p>Microsoft からは、EHCI コントローラーと xHCI コントローラーに接続されているデバイスと相互運用するドライバーのコア スタックが提供されます。</p>
<a href="supported-usb-classes.md" data-raw-source="[USB-IF device class drivers](supported-usb-classes.md)">USB-IF デバイス クラス ドライバー</a>
<p>Windows からは、USB-IF 認定のさまざまなデバイス クラス、オーディオ、大容量記憶装置などのインボックス デバイス クラス ドライバーが提供されます。</p>
<a href="winusb.md" data-raw-source="[USB generic function driver–WinUSB](winusb.md)">USB 汎用関数ドライバー - WinUSB</a>
<p>Windows からは、カスタム デバイスと複合デバイスの関数の関数ドライバーとして読み込まれる Winusb.sys が提供されます。</p>
<a href="usb-common-class-generic-parent-driver.md" data-raw-source="[USB generic parent driver for composite devices–Usbccgp](usb-common-class-generic-parent-driver.md)">複合デバイスの USB 汎用親ドライバー - Usbccgp</a>
<p>複数の関数を使う USB ドライバーのための親ドライバー。 Usbccgp では、これらの関数のそれぞれに対して物理デバイス オブジェクト (PDO) が作成されます。 個々の PDO はそれぞれの USB 関数ドライバーによって管理されます。これは Winusb.sys ドライバーか USB デバイス クラス ドライバーになります。</p>
<strong>USB ドライバーを開発するための WDF 拡張</strong>
<ul>
<li>USB コネクタ マネージャー クラス拡張 (UcmCx) 参照 <ul>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/" data-raw-source="[Ucmmanager.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/)">Ucmmanager.h</a>
    </li>
    </ul>
</li>
<li>USB ホスト コントローラー (UCX) 参照 <ul>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxclass/" data-raw-source="[Ucxclass.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxclass/)">Ucxclass.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxcontroller/" data-raw-source="[Ucxcontroller.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxcontroller/)">Ucxcontroller.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxroothub/" data-raw-source="[Ucxroothub.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/Ucxroothub/)">Ucxroothub.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxusbdevice/" data-raw-source="[Ucxusbdevice.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxusbdevice/)">Ucxusbdevice.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxendpoint/" data-raw-source="[Ucxendpoint.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxendpoint/)">Ucxendpoint.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxsstreams/" data-raw-source="[Ucxsstreams.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxsstreams/)">Ucxsstreams.h</a>
    </li>
    </ul>
</li>
<li>USB 関数クラス拡張 (UFX) 参照 <ul>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxbase/" data-raw-source="[Ufxbase.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxbase/)">Ufxbase.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxclient/" data-raw-source="[Ufxclient.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxclient/)">Ufxclient.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxproprietarycharger/" data-raw-source="[Ufxproprietarycharger.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxproprietarycharger/)">Ufxproprietarycharger.h</a>
    </li>
    </ul>
</li>
</ul>
<strong>Windows で USB デバイスをテストする</strong>
<p></p>
<a href="usb-driver-testing-guide.md" data-raw-source="[Testing USB hardware, drivers, and apps in Windows](usb-driver-testing-guide.md)">Windows で USB ハードウェア、ドライバー、アプリをテストする</a>
<p>USB ハードウェアまたはソフトウェアをテストするためのツールに関する情報を取得し、操作やその他のシステム イベントの足跡を記録し、クライアント ドライバーまたはアプリケーションによって送信された要求に USB ドライバー スタックがどのように応答するのかを観察します。</p>
<p>ハードウェア認証キットでテストの概要を読みます。ハードウェアのベンダーやデバイスのメーカーは自社の USB デバイスやホスト コントローラーを Windows ハードウェア認定のために提出するとき、このキットを利用して準備します。</p>
<p><strong>USB のためのその他のリソース</strong></p>
<a href="http://www.usb.org/developers/docs/" data-raw-source="[Official USB Specification](http://www.usb.org/developers/docs/)">公式の USB 仕様</a>
<p>USB プロトコルの技術的な詳細がすべて含まれています。</p>
<a href="https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/" data-raw-source="[Microsoft Windows USB Core Team Blog](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/)">Microsoft Windows USB コア チーム ブログ</a>
<p>Microsoft USB チームが記述した投稿をご覧ください。 このブログでは、Windows PC に搭載されたさまざまな USB ホスト コントローラーや USB ハブと連動する Windows USB ドライバー スタックを中心に取り上げています。 USB クライアント ドライバーの開発者や USB ハードウェアのデザイナーがドライバー スタック実装を理解し、一般的な問題を解決し、ツールを利用してトレースとログ ファイルを集める方法を説明する際に役立つリソース。</p>
<a href="https://community.osr.com/categories/ntdev" data-raw-source="[OSR Online Lists - ntdev](https://community.osr.com/categories/ntdev)">OSR オンライン リスト - ntdev</a>
<p>カーネルモード ドライバーの開発者のための <a href="http://www.osronline.com/index.cfm" data-raw-source="[OSR Online](http://www.osronline.com/index.cfm)">OSR オンライン</a>によって管理されるディスカッション リスト。</p>
<a href="https://msdn.microsoft.com/windows/hardware/" data-raw-source="[Windows Dev-Center for Hardware Development](https://msdn.microsoft.com/windows/hardware/)">ハードウェア開発のための Windows Dev-Center</a>
<p>Windows オペレーティング システムで動作する USB デバイスとドライバーを初めて開発する開発者からよく寄せられる質問に基づくその他のリソース。</p>
<p></p>
<p><strong>USB 関連の動画</strong></p>
<a href="http://channel9.msdn.com/Events/Build/2013/3-924a" data-raw-source="[UWP apps for USB devices](http://channel9.msdn.com/Events/Build/2013/3-924a)">USB デバイスの UWP アプリ</a>
<a href="http://channel9.msdn.com/events/BUILD/BUILD2011/HW-256T" data-raw-source="[Understanding USB 3.0 in Windows 8](http://channel9.msdn.com/events/BUILD/BUILD2011/HW-256T)">Windows 8 の USB 3.0 を理解する</a>
<a href="http://channel9.msdn.com/events/BUILD/BUILD2011/HW-773T" data-raw-source="[Building great USB 3.0 devices](http://channel9.msdn.com/events/BUILD/BUILD2011/HW-773T)">優れた USB 3.0 デバイスを開発する</a>
<a href="http://channel9.msdn.com/events/BUILD/BUILD2011/HW-258P" data-raw-source="[USB Debugging Innovations in Windows 8 (Part I, II, &amp; III)](http://channel9.msdn.com/events/BUILD/BUILD2011/HW-258P)">Windows 8 の USB デバッグの革新技術 (パート I、II、&amp; III)</a>
<p><strong>学習向け USB ハードウェア</strong></p>
<a href="microsoft-usb-test-tool--mutt--devices.md" data-raw-source="[MUTT devices](microsoft-usb-test-tool--mutt--devices.md)">MUTT デバイス</a>
<p>MUTT デバイス、SuperMUTT デバイス、付随するソフトウェア パッケージは USB テストの HCK スイートに統合されています。 USB のコントローラー、デバイス、システムの開発周期において、特にストレス テストにおいて使用できる自動化されたテストを提供します。</p>
<a href="http://www.osronline.com/index.cfm" data-raw-source="[OSR USB FX2 Learning Kit](http://www.osronline.com/index.cfm)">OSR USB FX2 ラーニング キット</a>
<p>USB ドライバーを初めて開発する場合。 このキットは、このドキュメント セットに含まれている学習用 USB サンプルに最も適しています。 OSR オンライン ストアからラーニング キットを入手できます。</p></td>
<td><strong>USB クライアント ドライバーを記述する (KMDF、UMDF)</strong>
<p>USB ドライバー開発の概要を紹介します。 デバイスに USB ドライバーを提供するために最も適したモデルを選択するための情報を提供します。 このセクションには、Microsoft Visual Studio に付属する USB テンプレートを使用し、初めてのユーザーモードおよびカーネルモード USB ドライバーを記述する方法をついてのチュートリアルも含まれています。</p>
<p><a href="getting-started-with-usb-client-driver-development.md" data-raw-source="[Getting started with USB client driver development](getting-started-with-usb-client-driver-development.md)">USB クライアント ドライバー開発の概要</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/" data-raw-source="[USB device driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/)">USB デバイス ドライバーのプログラミング参照</a></p>
<strong>USB ホスト コントローラー ドライバーを記述する</strong>
<p>仕様に準拠しない xHCI ホスト コントローラーを開発している場合、またはカスタムの非 xHCI ハードウェア (仮想ホスト コントローラーなど) を開発している場合、UCX と通信するホスト コントローラー ドライバーを記述できます。 たとえば、USB デバイスをサポートする無線ドックを検討してください。 PC は、トランスポートとして TCP 経由の USB を使用することで、無線ドック経由で USB デバイスと通信します。</p>
<p><a href="developing-windows-drivers-for-usb-host-controllers.md" data-raw-source="[Developing Windows drivers for USB host controllers](developing-windows-drivers-for-usb-host-controllers.md)">USB ホスト コントローラー用 Windows ドライバーの開発</a></p>
<p>
<ul>
<li>USB ホスト コントローラー (UCX) 参照 <ul>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxclass/" data-raw-source="[Ucxclass.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxclass/)">Ucxclass.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxcontroller/" data-raw-source="[Ucxcontroller.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxcontroller/)">Ucxcontroller.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxroothub/" data-raw-source="[Ucxroothub.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/Ucxroothub/)">Ucxroothub.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxusbdevice/" data-raw-source="[Ucxusbdevice.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxusbdevice/)">Ucxusbdevice.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxendpoint/" data-raw-source="[Ucxendpoint.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxendpoint/)">Ucxendpoint.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxsstreams/" data-raw-source="[Ucxsstreams.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ucxsstreams/)">Ucxsstreams.h</a>
    </li>
    </ul>
</li>
</ul>
</p>
<strong>USB デバイスの関数コントローラー ドライバーを記述する</strong>
<p>ホストによってデバイスに送信される USB データ転送とコマンドをすべて処理するコントローラー ドライバーを開発できます。 このドライバーは、Microsoft 提供の USB 関数コントローラー拡張 (UFX) と通信します。</p>
<p><a href="developing-windows-drivers-for-usb-function-controllers.md" data-raw-source="[Developing Windows drivers for USB function controllers](developing-windows-drivers-for-usb-function-controllers.md)">USB ファンクション コントローラー用 Windows ドライバーの開発</a></p>
<p>USB 関数クラス拡張 (UFX) 参照 <ul>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxbase/" data-raw-source="[Ufxbase.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxbase/)">Ufxbase.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxclient/" data-raw-source="[Ufxclient.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxclient/)">Ufxclient.h</a>
    </li>
    <li>
    <a href="https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxproprietarycharger/" data-raw-source="[Ufxproprietarycharger.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ufxproprietarycharger/)">Ufxproprietarycharger.h</a>
    </li>
    </ul>
</p>
<strong>USB Type-C コネクタ ドライバーを記述する</strong>
<p>Windows 10 には、新しい USB コネクタのサポートが導入されています。USB Type-C。 Microsoft 提供のクラス拡張モジュールと通信するコネクタのドライバーを記述できます。UcmCx は、どのポートで Type-C をサポートするか、どのポートで補助電源を与えるかなど、Type-C コネクタに関連するシナリオに対応します。</p>
<p><a href="developing-windows-drivers-for-usb-type-c-connectors.md" data-raw-source="[Developing Windows drivers for USB Type-C connectors](developing-windows-drivers-for-usb-type-c-connectors.md)">USB Type-C コネクタ用 Windows ドライバーの開発</a></p>
<p>USB コネクタ マネージャー クラス拡張 (UcmCx) 参照 <ul>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/" data-raw-source="[Ucmmanager.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/)">Ucmmanager.h</a>
    </li>
    </ul>
</p>
<strong>USB デュアルロール コントローラー ドライバーを記述する</strong>
<p>Windows 10 は USB デュアルロール コントローラー対応になりました。 Windows には、ChipIdea コントローラーと Synopsys コントローラーのためのインボックス クライアント ドライバーが含まれています。 その他のコントローラーの場合、デュアルロール クラス拡張 (UrsCx) とそのクライアント ドライバーが互いに通信し、デュアルロール コントローラーのロール切り替え機能を処理できるようにする一連のプログラミング インターフェイスが Microsoft から提供されます。</p>
<p>この機能の詳細については、以下を参照してください。</p>
<p><a href="usb-dual-role-driver-stack-architecture.md" data-raw-source="[USB Dual Role Driver Stack Architecture](usb-dual-role-driver-stack-architecture.md)">USB デュアル ロール ドライバー スタック アーキテクチャ</a></p>
<p>USB デュアルロール コントローラー ドライバーのプログラミング参照 <ul>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ursdevice/" data-raw-source="[Ursdevice.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ursdevice/)">Ursdevice.h</a>
    </li>
    </ul>
</p>
<strong>エミュレートされたデバイスの USB ドライバーを記述する</strong>
<p>Windows 10 では、エミュレートされたデバイスのサポートが導入されました。 エミュレートされた Universal Serial Bus (USB) ホスト コントローラー ドライバーと接続された仮想 USB デバイスを開発できるようになりました。 いずれのコンポーネントも、Microsoft 提供の USB デバイス エミュレーション クラス拡張 (UdeCx) と通信する 1 つの KMDF ドライバーに統合されます。</p>
<p><a href="developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md" data-raw-source="[Developing Windows drivers for emulated USB devices (UDE)](developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md)">列挙された USB デバイス (UDE) 用 Windows ドライバーの開発</a></p>
<p>エミュレートされた USB ホスト コントローラー ドライバーのプログラミング参照 <ul>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/" data-raw-source="[Udecxusbdevice.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/)">Udecxusbdevice.h</a>
    </li>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/" data-raw-source="[Udecxusbendpoint.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/)">Udecxusbendpoint.h</a>
    </li>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/" data-raw-source="[Udecxwdfdevice.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/)">Udecxusbdevice.h</a>
    </li>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/" data-raw-source="[Udecxurb.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/)">Udecxurb.h</a>
    </li>
    </ul>
</p>
<strong>UWP アプリを記述する</strong>
<p>UWP アプリで USB 機能を実装するための段階的手順を提供します。 USB デバイスにそのようなアプリを記述するには、Visual Studio と Microsoft Windows Software Development Kit (SDK) が必要です。</p>
<p><a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talk to USB devices, start to finish](talking-to-usb-devices-start-to-finish.md)">USB デバイスとの対話、開始から終了まで</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"><strong>Windows.Devices.Usb</strong></a></p>
<strong>Windows デスクトップ アプリを記述する</strong>
<p>アプリケーションが WinUSB 関数を呼び出し、USB デバイスと通信するしくみを説明します。</p>
<p><a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a WinUSB application](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB アプリケーションを記述する</a></p>
<p>WinUSB 関数 <ul>
    <li><a href="https://docs.microsoft.com/windows/desktop/api/winusb/" data-raw-source="[Winusb.h](https://docs.microsoft.com/windows/desktop/api/winusb/)">Winusb.h</a>
    </li>
    <li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/" data-raw-source="[Usbioctl.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/)">Usbioctl.h</a>
    </li>
    </ul>
</p>
<a href="wdk-resources-for-usb-driver-development.md" data-raw-source="[Common programming scenarios](wdk-resources-for-usb-driver-development.md)">一般的なプログラミング シナリオ</a>
<p>USB デバイスと通信する目的で、ドライバーまたはアプリが実行する一般的なタスクのリスト。 タスクごとに必要なプログラミング インターフェイスに関するクイック ヒントを取得します。</p>
<p></p>
<p><strong>USB サンプル</strong></p>
<p><a href="https://github.com/Microsoft/Windows-universal-samples" data-raw-source="[UWP app samples for USB](https://github.com/Microsoft/Windows-universal-samples)">USB の UWP アプリ サンプル</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=618021" data-raw-source="[Windows driver samples for USB](https://go.microsoft.com/fwlink/p/?linkid=618021)">USB の Windows ドライバー サンプル</a></p>
<p><strong>開発ツール</strong></p>
<a href="https://go.microsoft.com/fwlink/p/?linkid=619491" data-raw-source="[Download kits and tools for Windows]( https://go.microsoft.com/fwlink/p/?linkid=619491)">Windows 用のキットとツールのダウンロード</a></td>
</tr>
</tbody>
</table>

 

 

 





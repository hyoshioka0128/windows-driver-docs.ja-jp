---
Description: '目的: このセクションでは、Windows との相互運用が可能な USB デバイス ドライバーを開発できるように、Windows オペレーティングシステムでのユニバーサル シリアル バス (USB) のサポートについて説明します。'
title: USB デバイス用 Windows クライアント ドライバー開発の概要
ms.date: 01/07/2019
ms.localizationpriority: High
ms.openlocfilehash: a34a004df40b1c5b8bf8e7a0445047d7931a1a11
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843459"
---
# <a name="overview-of-developing-windows-client-drivers-for-usb-devices"></a>USB デバイス用 Windows クライアント ドライバー開発の概要


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは、Windows との相互運用が可能な USB デバイスドライバーを開発できるように、Windows オペレーティングシステムでのユニバーサル シリアル バス (USB) のサポートについて説明します。</p>
<p><strong>目的</strong></p>
<p>USB デバイスは、マウス デバイス、キーボードなどのように、1 つのポートを介してコンピューターに接続されている周辺機器です。 USB クライアント ドライバーは、デバイスが機能するようにハードウェアと通信するコンピューターにインストールされるソフトウェアです。 デバイスが Microsoft でサポートされているデバイス クラスに属している場合は、Windows により、デバイス用の <a href="system-supplied-usb-drivers.md" data-raw-source="[Microsoft-provided USB drivers](system-supplied-usb-drivers.md)">Microsoft 提供の USB ドライバー</a> (インボックス クラス ドライバー) の 1 つが読み込まれます。 それ以外の場合は、ハードウェアの製造元またはサードパーティ ベンダーからカスタム クライアント ドライバーが提供されている必要があります。 ユーザーは、Windows でデバイスが最初に検出されると、デバイス用のクライアント ドライバーをインストールします。 インストールが正常に終了すると、デバイスが接続されるたびに Windows でクライアント ドライバーが読み込まれ、デバイスがホスト コンピューターから切断されるとドライバーが読み込み解除されます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Frameworks](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows Driver Framework</a> (WDF) または <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model" data-raw-source="[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)">Windows Driver Model</a> (WDM) を使用して、USB デバイス用のカスタム クライアント ドライバーを開発できます。 ほとんどのクライアント ドライバーでは、ハードウェアとの間で直接通信が行われるのではなく、Microsoft が提供する USB ドライバー スタックに要求が送信されます。このスタックにより、ハードウェア アブストラクション レイヤー (HAL) 関数が呼び出されて、ハードウェアにクライアント ドライバーの要求が送信されます。 このセクションのトピックでは、クライアント ドライバーで送信できる一般的な要求と、クライアント ドライバーでこれらの要求を作成するために呼び出す必要があるデバイス ドライバー インターフェイス (DDI) について説明します。</p>
<p><strong>対象となる開発者</strong></p>
<p>USB デバイス用のクライアント ドライバーは、USB ドライバー スタックによって公開されている DDI を介してデバイスと通信する WDF ドライバーまたは WDM ドライバーです。 このセクションは、WDM に精通している C/C++ プログラマーを対象としています。 このセクションを使用する前に、基本的なドライバーの開発について理解しておく必要があります。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index" data-raw-source="[Getting Started with Windows Drivers](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index)">Windows ドライバーの概要</a>」を参照してください。 WDF ドライバーの場合、クライアント ドライバーでは、USB ターゲットを操作するために特別に設計された<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)">カーネルモード ドライバー フレームワーク</a> (KMDF) インターフェイスまたは<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[User-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">ユーザー モード ドライバー フレームワーク</a> (UMDF) インターフェイスを使用できます。 USB 固有のインターフェイスの詳細については、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/" data-raw-source="[WDF USB Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/)">WDF USB リファレンス</a>および <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/" data-raw-source="[UMDF USB I/O Target Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/)">UMDF USB I/O ターゲット インターフェイス</a>に関するページを参照してください。</p>
<p><strong>開発ツール</strong></p>
<p>Windows Driver Kit (WDK) には、ヘッダー、ライブラリ、ツール、サンプルなど、ドライバーの開発に必要なリソースが含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p>
<p><strong>USB プログラミング リファレンス</strong></p>
<p>USB クライアント ドライバーで使用される I/O 要求、サポート ルーチン、構造、およびインターフェイスの仕様を提供します。 これらのルーチンおよび関連するデータ構造は、WDK ヘッダーで定義されています。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#common-usb-client-driver-reference" data-raw-source="[Universal Serial Bus (USB) programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#common-usb-client-driver-reference)">ユニバーサル シリアル バス (USB) プログラミング リファレンス</a>。</p>
<p><strong>USB ドライバーのサンプル</strong></p>
<p>これらのサンプルを使用して、USB クライアント ドライバーのプログラミングを開始します。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617157" data-raw-source="[Usbsamp Generic USB Driver]( https://go.microsoft.com/fwlink/p/?linkid=617157)">USBSAMP 汎用 USB ドライバー</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617158" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?linkid=617158)">OSR USB-FX2 用の KMDF 関数ドライバーのサンプル</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR USB-FX2 用の UMDF 関数ドライバーのサンプル</a></li>
</ul>
<p><strong>関連する標準と仕様</strong></p>
<p>公式の USB 仕様は、<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">ユニバーサル シリアル バスのドキュメント</a>の Web サイトからダウンロードできます。 この Web サイトには、ユニバーサル シリアル バス リビジョン 3.0 仕様とユニバーサル シリアル バス リビジョン 2.0 仕様へのリンクが含まれています。</p></td>
<td><p><strong>ドキュメントのセクション</strong></p>
<p><a href="getting-started-with-usb-client-driver-development.md" data-raw-source="[Getting started with USB client driver development](getting-started-with-usb-client-driver-development.md)">USB クライアント ドライバー開発の概要</a></p>
USB ドライバー開発の概要を紹介します。 デバイスに USB ドライバーを提供するために最も適したモデルを選択するための情報を提供します。
Microsoft Visual Studio に付属する USB テンプレートを使用して、初めてのスケルトン ユーザーモードおよびカーネルモードの USB ドライバーを記述、ビルド、およびインストールします。
<p><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows の USB ホスト側ドライバー</a></p>
USB ドライバー スタックのアーキテクチャの概要を示します。
<p><a href="communicating-with-a-usb-device.md" data-raw-source="[About USB Block Requests (URBs)](communicating-with-a-usb-device.md)">USB 要求ブロック (URB) について</a></p>
USB ドライバー スタックに要求を送信するために、クライアント ドライバーで USB 要求ブロック (URB) と呼ばれる可変長データ構造を構築する方法について説明します。
<p><a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB 記述子</a></p>
USB ドライバー スタックに要求を送信するために、クライアント ドライバーで USB 要求ブロック (URB) と呼ばれる可変長データ構造を構築する方法について説明します。
<p><a href="configuring-usb-devices.md" data-raw-source="[Selecting a USB configuration in USB drivers](configuring-usb-devices.md)">USB ドライバーでの USB 構成の選択</a></p>
デバイス構成とは、クライアント ドライバーで各インターフェイスの USB 構成と代替インターフェイスを選択するために実行するタスクを指します。 このセクションでは、USB 構成を選択するために必要なメソッド呼び出しを紹介します。
<p><a href="usb-device-i-o.md" data-raw-source="[Sending USB data transfers in USB client drivers](usb-device-i-o.md)">USB クライアント ドライバーでの USB データ転送の送信</a></p>
USB パイプ、I/O 要求の URB のほか、クライアント ドライバーでデバイス ドライバー インターフェイス (DDI) を使用して USB デバイスとの間でデータを転送する方法について説明します。
<p><a href="usb-power-management.md" data-raw-source="[Implementing power management in USB client drivers](usb-power-management.md)">USB クライアント ドライバーでの電源管理の実装</a></p>
ユニバーサル シリアル バス (USB) 仕様に準拠している USB デバイスの電源管理機能には、豊富で複雑な一連の電源管理機能が備わっています。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  




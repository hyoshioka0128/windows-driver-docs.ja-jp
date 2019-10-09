---
Description: PurposeThis セクションでは、windows との相互運用が可能な USB デバイスドライバーを開発できるように、Windows オペレーティングシステムでのユニバーサルシリアルバス (USB) のサポートについて説明します。
title: USB デバイス用 Windows クライアント ドライバー開発の概要
ms.date: 01/07/2019
ms.localizationpriority: High
ms.openlocfilehash: cf22c8f52593963befb5502c97d536acb054593e
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007566"
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
<p>このセクションでは、windows との相互運用が可能な USB デバイスドライバーを開発できるように、Windows オペレーティングシステムでの Universal Serial Bus (USB) のサポートについて説明します。</p>
<p><strong>該当する場合</strong></p>
<p>USB デバイスは、1つのポートを介してコンピューターに接続されている周辺機器 (マウスデバイス、キーボードなど) です。 USB クライアントドライバーは、デバイスが機能するようにハードウェアと通信するコンピューターにインストールされるソフトウェアです。 デバイスが Microsoft によってサポートされるデバイスクラスに属している場合、Windows は、デバイスの<a href="system-supplied-usb-drivers.md" data-raw-source="[Microsoft-provided USB drivers](system-supplied-usb-drivers.md)">microsoft 提供の USB ドライバー</a> (インボックスクラスのドライバー) の1つを読み込みます。 それ以外の場合は、カスタムクライアントドライバーがハードウェアの製造元またはサードパーティベンダーから提供されている必要があります。 ユーザーは、デバイスが最初に Windows によって検出されたときに、デバイスのクライアントドライバーをインストールします。 インストールが正常に終了すると、デバイスが接続されるたびに Windows によってクライアントドライバーが読み込まれ、デバイスがホストコンピューターからデタッチされたときにドライバーがアンロードされます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Frameworks](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows ドライバーフレームワーク</a>(WDF) または<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model" data-raw-source="[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)">Windows Driver Model</a> (WDM) を使用して、USB デバイス用のカスタムクライアントドライバーを開発することができます。 ハードウェアと直接通信するのではなく、ほとんどのクライアントドライバーは、ハードウェアアブストラクションレイヤー (HAL) 関数を呼び出してハードウェアにクライアントドライバーの要求を送信する、Microsoft が提供する USB ドライバースタックに要求を送信します。 このセクションのトピックでは、クライアントドライバーが送信できる一般的な要求と、クライアントドライバーがこれらの要求を作成するために呼び出す必要があるデバイスドライバーインターフェイス (DDIs) について説明します。</p>
<p><strong>開発者向け</strong></p>
<p>USB デバイス用のクライアントドライバーは、USB ドライバースタックによって公開されている DDIs を介してデバイスと通信する WDF または WDM ドライバーです。 このセクションは、WDM に精通してC++いる C/プログラマーが使用することを目的としています。 このセクションを使用する前に、基本的なドライバーの開発について理解しておく必要があります。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index" data-raw-source="[Getting Started with Windows Drivers](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index)">Windows ドライバーでのはじめに</a>」を参照してください。 WDF ドライバーの場合、クライアントドライバーは、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)">カーネルモードドライバーフレームワーク</a>(kmdf)、または USB ターゲットを操作するために特別に設計された<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[User-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">ユーザーモードドライバーフレームワーク</a>(UMDF) インターフェイスを使用できます。 USB 固有のインターフェイスの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/" data-raw-source="[WDF USB Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)">WDF Usb Reference</a> AND <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/" data-raw-source="[UMDF USB I/O Target Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/)">UMDF Usb i/o Target インターフェイス</a>」を参照してください。</p>
<p><strong>開発ツール</strong></p>
<p>Windows Driver Kit (WDK) には、ドライバーの開発に必要なリソース (ヘッダー、ライブラリ、ツール、サンプルなど) が含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p>
<p><strong>USB プログラミングリファレンス</strong></p>
<p>は、USB クライアントドライバーが使用する i/o 要求、サポートルーチン、構造体、およびインターフェイスの仕様を提供します。 これらのルーチンと関連するデータ構造は、WDK ヘッダーで定義されています。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#common-usb-client-driver-reference" data-raw-source="[Universal Serial Bus (USB) programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#common-usb-client-driver-reference)">ユニバーサルシリアルバス (USB) プログラミングリファレンス</a>。</p>
<p><strong>USB ドライバーのサンプル</strong></p>
<p>これらのサンプルを使用して、USB クライアントドライバーのプログラミングを開始します。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617157" data-raw-source="[Usbsamp Generic USB Driver]( https://go.microsoft.com/fwlink/p/?linkid=617157)">Usbsamp 汎用 USB ドライバー</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617158" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?linkid=617158)">OSR USB 用 KMDF 関数ドライバーのサンプル FX2</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR USB 用の UMDF 関数ドライバーのサンプル FX2</a></li>
</ul>
<p><strong>関連する標準と仕様</strong></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">ユニバーサルシリアルバスドキュメント</a>の web サイトから、公式の USB 仕様をダウンロードできます。 この web サイトには、ユニバーサルシリアルバスリビジョン3.0 仕様と、Universal Serial Bus リビジョン2.0 仕様へのリンクが含まれています。</p></td>
<td><p><strong>ドキュメントのセクション</strong></p>
<p><a href="getting-started-with-usb-client-driver-development.md" data-raw-source="[Getting started with USB client driver development](getting-started-with-usb-client-driver-development.md)">USB クライアント ドライバー開発の概要</a></p>
USB ドライバー開発の概要を紹介します。 デバイスに USB ドライバーを提供するために最も適したモデルを選択するための情報を提供します。
Microsoft Visual Studio に含まれている USB テンプレートを使用して、初めてのユーザーモードおよびカーネルモードの USB ドライバーを作成、ビルド、およびインストールします。
<p><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows の USB ホスト側ドライバー</a></p>
USB ドライバーのスタックアーキテクチャの概要について説明します。
<p><a href="communicating-with-a-usb-device.md" data-raw-source="[About USB Block Requests (URBs)](communicating-with-a-usb-device.md)">USB ブロック要求について (URBs)</a></p>
Usb ドライバースタックに要求を送信するために、クライアントドライバーが USB 要求ブロック (URB) と呼ばれる可変長データ構造を構築する方法について説明します。
<p><a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB 記述子</a></p>
Usb ドライバースタックに要求を送信するために、クライアントドライバーが USB 要求ブロック (URB) と呼ばれる可変長データ構造を構築する方法について説明します。
<p><a href="configuring-usb-devices.md" data-raw-source="[Selecting a USB configuration in USB drivers](configuring-usb-devices.md)">USB ドライバーで USB 構成を選択する</a></p>
デバイス構成とは、クライアントドライバーが USB 構成と各インターフェイスの代替インターフェイスを選択するために実行するタスクを指します。 このセクションは、USB 構成を選択するために必要なメソッド呼び出しを示しています。
<p><a href="usb-device-i-o.md" data-raw-source="[Sending USB data transfers in USB client drivers](usb-device-i-o.md)">USB クライアントドライバーでの USB データ転送の送信</a></p>
USB パイプ、i/o 要求の URBs、およびクライアントドライバーがデバイスドライバーインターフェイス (DDIs) を使用して USB デバイスとの間でデータを転送する方法について説明します。
<p><a href="usb-power-management.md" data-raw-source="[Implementing power management in USB client drivers](usb-power-management.md)">USB クライアントドライバーでの電源管理の実装</a></p>
ユニバーサルシリアルバス (USB) 仕様に準拠している USB デバイスの電源管理機能を使用すると、豊富で複雑な電源管理機能を使用できます。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  




---
Description: PurposeThis セクションでは Windows と相互運用可能な USB デバイス ドライバーを開発するように、Windows オペレーティング システムでのユニバーサル シリアル バス (USB) のサポートについて説明します。
title: USB デバイス用 Windows クライアント ドライバーの開発
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: b0c34a7025bbf4e43d1fec7b77ab8b3122444baa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373459"
---
# <a name="developing-windows-client-drivers-for-usb-devices"></a>USB デバイス用 Windows クライアント ドライバーの開発


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは Windows と相互運用可能な USB デバイス ドライバーを開発するように、Windows オペレーティング システムでのユニバーサル シリアル バス (USB) のサポートについて説明します。</p>
<p><strong>該当する場合</strong></p>
<p>USB デバイスは、1 つのポート経由でコンピューターに接続されているキーボード、マウス デバイスなどの周辺機器です。 USB クライアント ドライバーは、デバイスの機能を作成するためのハードウェアと通信するコンピューターにインストールされているソフトウェアです。 Windows ロードのいずれかの場合は、デバイスは、Microsoft でサポートされているデバイス クラスに属している、 <a href="system-supplied-usb-drivers.md" data-raw-source="[Microsoft-provided USB drivers](system-supplied-usb-drivers.md)">Microsoft 提供の USB ドライバー</a> (インボックス クラス ドライバー) デバイス。 それ以外の場合、カスタムのクライアント ドライバーは、ハードウェアの製造元によって提供される必要があります。 またはサード パーティ ベンダー。 デバイスが最初に Windows によって検出されたときに、ユーザーは、デバイスのクライアント ドライバーをインストールします。 インストールの成功後、デバイスが接続されているし、デバイスが、ホスト コンピューターからデタッチされると、ドライバーをアンロードするたびに、Windows は、クライアント ドライバーを読み込みます。</p>
<p>使用して、USB デバイス用のカスタム クライアント ドライバーを開発することができます、 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Frameworks](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows Driver Frameworks</a> (WDF) または<a href="https://msdn.microsoft.com/library/windows/hardware/ff565698" data-raw-source="[Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698)">Windows Driver Model</a> (WDM)。 ハードウェアと直接通信しているのではなくは、ほとんどのクライアント ドライバーは、ハードウェアに、クライアント ドライバーの要求を送信するハードウェア アブストラクション レイヤー (HAL) 関数呼び出しを実行する Microsoft 提供の USB ドライバー スタックに、要求を送信します。 このセクションのトピックでは、クライアント ドライバーを送信できる一般的な要求とそれらの要求を作成するクライアント ドライバーを呼び出す必要のあるデバイス ドライバー インターフェイス (Ddi) について説明します。</p>
<p><strong>対象となる開発者</strong></p>
<p>USB デバイスのクライアント ドライバーは、USB ドライバー スタックによって公開される Ddi を使用して、デバイスと通信する WDF または WDM ドライバーです。 このセクションでは、WDM に慣れている C/C++ プログラマ用ものです。 このセクションを使用する前に、基本的なドライバーの開発を理解する必要があります。 詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554690" data-raw-source="[Getting Started with Windows Drivers](https://msdn.microsoft.com/library/windows/hardware/ff554690)">Windows ドライバーの概要</a>します。 WDF ドライバーでは、クライアント ドライバーを使用できます<a href="https://msdn.microsoft.com/library/windows/hardware/ff551869" data-raw-source="[Kernel-Mode Driver Framework](https://msdn.microsoft.com/library/windows/hardware/ff551869)">カーネル モード ドライバー フレームワーク</a>(KMDF) または<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[User-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">ユーザー モード ドライバー フレームワーク</a>(UMDF) インターフェイスが USB ターゲットを持つ操作専用に設計されています。 USB に固有のインターフェイスの詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/dn265671" data-raw-source="[WDF USB Reference](https://msdn.microsoft.com/library/windows/hardware/dn265671)">WDF USB 参照</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff561332" data-raw-source="[UMDF USB I/O Target Interfaces](https://msdn.microsoft.com/library/windows/hardware/ff561332)">UMDF USB I/O ターゲット インターフェイス</a>します。</p>
<p><strong>開発ツール</strong></p>
<p>Windows Driver Kit (WDK) には、ヘッダー、ライブラリ、ツール、およびサンプルなど、ドライバーの開発に必要なリソースが含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p>
<p><strong>USB のプログラミング リファレンス</strong></p>
<p>I/O 要求、サポート ルーチン、構造、および USB クライアント ドライバーによって使用されるインターフェイスの仕様を示します。 これらのルーチンと関連のデータ構造は、WDK ヘッダーで定義されます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#common-usb-client-driver-reference" data-raw-source="[Universal Serial Bus (USB) programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#common-usb-client-driver-reference)">ユニバーサル シリアル バス (USB) プログラミング リファレンス</a>します。</p>
<p><strong>USB ドライバーのサンプル</strong></p>
<p>USB クライアント ドライバーのプログラミングを開始するには、これらのサンプルを使用します。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617157" data-raw-source="[Usbsamp Generic USB Driver]( https://go.microsoft.com/fwlink/p/?linkid=617157)">Usbsamp 汎用 USB ドライバー</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617158" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?linkid=617158)">OSR usb-fx2 のサンプル KMDF 関数ドライバー</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR usb-fx2 のサンプル UMDF 関数ドライバー</a></li>
</ul>
<p><strong>関連の標準および仕様</strong></p>
<p>公式の USB 仕様をダウンロードすることができます、<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">ユニバーサル シリアル バス ドキュメント</a>web サイト。 この web サイトには、ユニバーサル シリアル バス リビジョン 3.0 仕様と、ユニバーサル シリアル バスのリビジョン 2.0 仕様へのリンクが含まれています。</p></td>
<td><p><strong>ドキュメントのセクション</strong></p>
<p><a href="getting-started-with-usb-client-driver-development.md" data-raw-source="[Getting started with USB client driver development](getting-started-with-usb-client-driver-development.md)">USB クライアント ドライバー開発の概要</a></p>
USB ドライバー開発の概要を紹介します。 デバイスに USB ドライバーを提供するために最も適したモデルを選択するための情報を提供します。
作成、ビルド、および Microsoft Visual Studio に含まれている USB テンプレートを使用して最初スケルトン ユーザー モードとカーネル モード USB ドライバーをインストールします。
<p><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows での USB ホスト側のドライバー</a></p>
USB ドライバー スタックのアーキテクチャの概要を示します。
<p><a href="communicating-with-a-usb-device.md" data-raw-source="[About USB Block Requests (URBs)](communicating-with-a-usb-device.md)">USB ブロック要求 (翻訳) について</a></p>
クライアント ドライバーが、USB 要求ブロック (URB) USB ドライバー スタックへの要求を送信すると呼ばれる可変長のデータ構造を構築する方法について説明します。
<p><a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB ディスクリプター</a></p>
クライアント ドライバーが、USB 要求ブロック (URB) USB ドライバー スタックへの要求を送信すると呼ばれる可変長のデータ構造を構築する方法について説明します。
<p><a href="configuring-usb-devices.md" data-raw-source="[Selecting a USB configuration in USB drivers](configuring-usb-devices.md)">USB ドライバーで USB 構成の選択</a></p>
デバイスの構成には、各インターフェイスで、USB 構成、および代替インターフェイスを選択するクライアント ドライバーを実行するタスク。 セクションは、USB 構成を選択するために必要なメソッドの呼び出しを示します。
<p><a href="usb-device-i-o.md" data-raw-source="[Sending USB data transfers in USB client drivers](usb-device-i-o.md)">USB クライアント ドライバーでの USB データ転送の送信</a></p>
USB パイプ、I/O 要求の場合の翻訳、およびクライアント ドライバーがデバイス ドライバー インターフェイス (Ddi) を使用して、USB デバイスとの間のデータを転送する方法について説明します。
<p><a href="usb-power-management.md" data-raw-source="[Implementing power management in USB client drivers](usb-power-management.md)">USB クライアント ドライバーでの電源管理の実装</a></p>
電源管理機能のセットを使用して、リッチで複雑なユニバーサル シリアル バス (USB) 仕様に準拠している USB デバイスの電源管理機能があります。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  




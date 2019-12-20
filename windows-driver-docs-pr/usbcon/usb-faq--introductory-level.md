---
Description: このトピックでは、Windows オペレーティングシステムで USB デバイスとドライバーを開発して統合することを初めて行うドライバー開発者に関してよく寄せられる質問を示します。
title: Windows における USB- よくあるご質問
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280052d878eeb9ffd367fc43039a7d22c9332d6e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210622"
---
# <a name="usb-in-windows---faq"></a>Windows における USB- よくあるご質問

このトピックでは、Windows オペレーティングシステムで USB デバイスとドライバーを開発して統合することを初めて行うドライバー開発者に関してよく寄せられる質問を示します。

- [ほぼ同じように、多数の USB 用語がスローされました。どのような意味があるのでしょうか。](#i-hear-numerous-usb-terms-thrown-around-almost-interchangeably-what-do-they-all-mean)
- [PC に USB 3.0 ポートがありますか。](#does-my-pc-have-usb-30-ports)
- [拡張可能なホストコントローラーのドライバーをインストールする必要がありますか。](#do-i-need-to-install-drivers-for-my-extensible-host-controller)
- [システムに複数のホストコントローラーが表示されるのはなぜですか。](#why-do-i-see-several-host-controllers-on-my-system)
- [USB 3.0 ハブを1つしか接続していない場合、デバイスマネージャーに2つのハブが表示されるのはなぜですか。](#why-do-i-see-two-hubs-in-device-manager-when-i-have-connected-only-one-usb-30-hub)
- [2.0 ポートに接続されているデバイス用に読み込まれるドライバーのセットを教えてください。](#which-set-of-drivers-is-loaded-for-the-devices-that-are-connected-to-20-ports)
- [USB 3.0 デバイスが SuperSpeed として動作しているかどうかを判断操作方法には](#how-do-i-determine-whether-my-usb-30-device-is-operating-as-superspeed)
- [SuperSpeed USB デバイスが同等の高速 USB デバイスより高速ではないのはなぜですか。](#why-isnt-my-superspeed-usb-device-faster-than-an-equivalent-high-speed-usb-device)
- [1つのハードウェアに複合デバイスと複合デバイスを用意することはできますか。](#is-it-possible-to-have-a-composite-and-a-compound-device-in-one-piece-of-hardware)
- [新しいポートに移動すると、USB デバイスの一部が再インストールされるのはなぜですか。](#why-are-some-of-my-usb-devices-reinstalled-when-they-are-moved-to-a-new-port)
- [USB 製品パッケージの設計に関する推奨事項の一覧がありますか。](#is-there-a-list-of-design-recommendations-for-usb-product-packaging)
- [USB 3.0 デバイスをサポートするようにクライアントドライバーを書き換える必要がありますか。](#do-i-have-to-rewrite-my-client-driver-to-support-usb-30-devices)
- [SuperSpeed ストレージデバイスで使用されているドライバー (Uaspstor または Usbstor.sys)](#which-driver-is-loaded-for-my-superspeed-storage-device-use-uaspstorsys-or-usbstorsys)
- [Microsoft はどの USB DWG クラスをサポートしていますか。](#which-usb-dwg-classes-does-microsoft-support)
- [カスタム USB デバイスにどのデバイスセットアップクラスを使用する必要がありますか。](#which-device-setup-class-should-i-use-for-a-custom-usb-device)
- [USB デバイスを接続したときに CPU が C3 にならないのはなぜですか。](#why-wont-my-cpu-enter-c3-when-i-attach-some-usb-devices)
- [セレクティブサスペンドをサポートする USB クラスドライバー](#which-usb-class-drivers-support-selective-suspend)
- [USB デバイスが S3 から Windows を目覚めできないのはなぜですか。](#why-cant-a-usb-device-awaken-windows-from-s3)
- [Enhanced (USB 2.0) ホストコントローラーのドライバーをインストールする必要がありますか。](#do-i-need-to-install-drivers-for-my-enhanced-usb-20-host-controller)
- ["高速ではない USB ポートに接続されている高速 USB デバイス" という通知を無効にすることはできますか。](#can-i-disable-the-hi-speed-usb-device-plugged-into-non-hi-speed-usb-port-notice)
- [USB 2.0 ハブのシングル TT またはマルチ TT ですか。](#is-my-usb-20-hub-single-tt-or-multi-tt)
- [USB シリアル番号で有効な文字またはバイトは何ですか。](#what-characters-or-bytes-are-valid-in-a-usb-serial-number)
- [Windows のローカライズされたビルドにおける文字列要求では、どのような LANGID が使用されますか。](#what-langid-is-used-in-a-string-request-on-localized-builds-of-windows)
- [デバイスのシリアル番号を抽出するために使用される LANGID](#what-langid-is-used-to-extract-a-devices-serial-number)
- [さまざまな Windows バージョンの USB 転送の最大サイズはどのくらいですか。](#what-is-the-maximum-usb-transfer-size-for-different-windows-versions)
- [複合デバイスの複数のインターフェイスに番号を割り当てる方法](#how-should-numbers-be-assigned-to-multiple-interfaces-on-a-composite-device)
- [Usbccgp によって課せられる主な制限は何ですか。](#what-are-the-major-restrictions-imposed-by-usbccgpsys)
- [USB コアバイナリのデバッグトレースを有効に操作方法ますか?](#how-do-i-enable-debug-tracing-for-usb-core-binaries)
- [Windows はインターフェイスの関連付け記述子をサポートしていますか。](#does-windows-support-interface-association-descriptors)
- [USB スタックはチェーンされた MDLs を URB に処理しますか。](#does-the-usb-stack-handle-chained-mdls-in-a-urb)
- [ドライバーが1つの IRP に複数の URB を持つことはできますか。](#can-a-driver-have-more-than-one-urb-in-an-irp)
- [Windows では USB 複合ハブがサポートされるのですか。](#does-windows-support-usb-composite-hubs)

## <a name="i-hear-numerous-usb-terms-thrown-around-almost-interchangeably-what-do-they-all-mean"></a>ほぼ同じように、多数の USB 用語がスローされました。 どのような意味があるのでしょうか。

たとえば、「 *usb 3.0 のおかげで、SUPERSPEED usb thumb ドライブを PC の xHCI ホストコントローラーに接続して、ファイルをより速くコピーすることができます」* というようなものがあるとします。

その文での USB 用語について説明します。 Usb 3.0、USB 2.0、および USB 1.0 は、usb[実装者フォーラム](https://www.usb.org/)の usb 仕様のリビジョン番号を参照しています。 USB 仕様では、ホスト PC と USB デバイスが相互に通信する方法を定義します。

バージョン番号は、最大転送速度も示しています。 最新仕様のリビジョンは USB 3.0 で、最大転送速度は 5 Gbps です。 USB 1.0 では、低速 USB (最大 1.5 Mbps) とフルスピード USB (最大 12 Mbps) の2種類のデータ速度が定義されています。 USB 2.0 では、高速および高速のデバイスのサポートを維持しながら、新しいデータ速度、高速 USB (480 Mbps) が定義されています。 USB 3.0 は、以前に定義されたすべてのデータ速度で動作し続けます。 製品パッケージを見ると、SuperSpeed USB は最新の USB 3.0 デバイスを参照します。 高速 usb は、高速 USB 2.0 デバイスを記述するために使用されます。 記述子のない USB は、低速デバイスと完全速度デバイスを指します。

Usb プロトコルに加えて、USB ホストコントローラーには、デバイスが接続されている PC のハードウェアの2番目の仕様があります。 ホストコントローラーのインターフェイス仕様では、ホストコントローラーのハードウェアとソフトウェアがどのように対話するかを定義します。 拡張可能なホストコントローラーインターフェイス (xHCI) は、USB 3.0 ホストコントローラーを定義します。 Enhanced Host Controller Interface (EHCI) は、USB 2.0 ホストコントローラーを定義します。 ユニバーサルホストコントローラー (UHCI) と Open Host Controller (OHCI) は、USB 1.0 ホストコントローラーの2つの代替実装です。

## <a name="does-my-pc-have-usb-30-ports"></a>PC に USB 3.0 ポートがありますか。

USB 3.0 ポートは SuperSpeed USB ロゴでマークされているか、通常は青色で示されます。

![usb ロゴ付きのポート](images/usb-intro-faq-fig1-usblogo.png)

![blue usb 3.0 ポート](images/usb-intro-faq-fig2-blueusbport.png)

新しい Pc には、USB 3.0 と USB 2.0 の両方のポートがあります。 SuperSpeed USB デバイスが最高速度で実行されるようにするには、USB 3.0 ポートを見つけて、そのポートにデバイスを接続します。 USB 2.0 ポートに接続されている SuperSpeed デバイスは、高速で動作します。

また、デバイスマネージャーで特定のポートが USB 3.0 ポートであることを確認することもできます。 Windows Vista 以降のバージョンの Windows では、デバイスマネージャーを開き、一覧からポートを選択します。

![デバイスマネージャーの usb ホストコントローラー](images/usb-host-controllers-dm.png)

拡張可能なホストコントローラーがある場合は、USB 3.0 がサポートされます。

## <a name="do-i-need-to-install-drivers-for-my-extensible-host-controller"></a>拡張可能なホストコントローラーのドライバーをインストールする必要がありますか。

Windows 8 および Windows Server 2012 には、USB 3.0 のサポートが含まれています。

PC に USB 3.0 ポートがあり、Windows 8 より前のバージョンの Windows を実行している場合、ホストコントローラードライバーは PC の製造元から提供されます。 これらのドライバーを再インストールする必要がある場合は、製造元から入手する必要があります。

Windows 8 より前のバージョンの Windows を実行している PC に USB 3.0 コントローラーカードを追加した場合は、コントローラーカードの製造元から提供されているドライバーをインストールする必要があります。

Windows 8 では、Microsoft が提供する一連の USB 3.0 ドライバー (USB ドライバースタック) は、ほとんどのホストコントローラーで動作します。 Microsoft USB 3.0 ドライバースタックは、Fresco Logic FL1000 コントローラーでは機能しません。 FL1000 コントローラーがあるかどうかを判断するには、デバイスマネージャーを開き、[**ユニバーサルシリアルバスコントローラー**] を展開します。 コントローラーのプロパティを表示するには、コントローラーノードを右クリックします。 [**詳細**] タブの一覧で、[**ハードウェア id** ] プロパティを選択します。 ハードウェア ID が PCI\\VEN\_1B73 & DEV\_1000 で始まる場合は、これが FL1000 です。 そのコントローラーについては、PC またはコントローラーカードの製造元からドライバーをダウンロードしてインストールしてください。

## <a name="why-do-i-see-several-host-controllers-on-my-system"></a>システムに複数のホストコントローラーが表示されるのはなぜですか。

PC に接続する USB デバイスに加えて、web カメラ、指紋リーダー、SD カードリーダーなど、USB 経由で接続される可能性のある多数のデバイスが PC 内に統合されています。 これらのデバイスをすべて接続し、外部 USB ポートを引き続き提供するために、PC は複数の USB ホストコントローラーをサポートしています。

USB 3.0 xHCI ホストコントローラーは、すべての USB デバイス速度、SuperSpeed、高速、最高速度、および低速度と完全に下位互換性があります。 任意のデバイスを直接 xHCI コントローラーに接続し、そのデバイスが動作することを期待できます。 EHCI コントローラーでは、そうではありません。 USB 2.0 仕様では、すべての速度のデバイスがサポートされていますが、EHCI コントローラーでは高速 USB デバイスのみがサポートされています。 高速で高速な USB デバイスを動作させるには、USB 2.0 ハブを介して EHCI コントローラーに接続されているか、UHCI または OHCI コントローラーに接続されている必要があります。

新しい Pc では、Pc によって公開されるほとんどの USB 2.0 ポートは、USB 2.0 ハブの下流にあります。 このハブは EHCI コントローラーに接続されています。 これにより、PC の USB 2.0 ポートは、あらゆる速度のデバイスで動作できるようになります。 SuperSpeed デバイスは、2.0 ポートに接続しているときに高速デバイスとして動作します。

USB 2.0 仕様がリリースされた後、Pc は、すべての速度のデバイスをサポートするために、ホストコントローラーを組み合わせて使用しました。 単一の USB 2.0 ポートは、EHCI ホストコントローラーと UHCI または OHCI ホストコントローラーの2つのホストコントローラーに接続されます。 デバイスを接続すると、その接続は2つのホストのいずれかに動的にルーティングされます。 ルーチンは、デバイスの速度に依存します。

## <a name="why-do-i-see-two-hubs-in-device-manager-when-i-have-connected-only-one-usb-30-hub"></a>USB 3.0 ハブを1つしか接続していない場合、デバイスマネージャーに2つのハブが表示されるのはなぜですか。

XHCI ホストコントローラーは、デバイスの速度で動作しますが、SuperSpeed hub は SuperSpeed デバイスでのみ機能します。 USB 3.0 ハブがすべての速度で動作することを保証するために、SuperSpeed ハブと USB 2.0 ハブの2つの部分があります。 USB 3.0 hub は、デバイスの速度に基づいて、SuperSpeed hub または 2.0 hub にデバイスを動的にルーティングすることで、すべての速度をサポートできます。

デバイスマネージャーを開き、**接続別にデバイス**を表示し、拡張可能なホストコントローラーを見つけます。 1つの USB 3.0 ハブを USB 3.0 ポートに接続すると、コントローラーのルートハブの下流に2つのハブがあります。

![デバイスマネージャーの usb 3.0 ハブ](images/usb-3-hub-dm.png)

次の例では、SuperSpeed USB ストレージデバイスと USB オーディオデバイスが両方とも USB 3.0 ハブに接続されています。 ストレージデバイスが SuperSpeed ハブの下流にあり、オーディオデバイスが USB 2.0 ハブの下流にあることを確認できます。

![デバイスマネージャーでデバイスが接続されている usb 3.0 ハブ](images/usb-3-hub-connected-devices-dm.png)

## <a name="which-set-of-drivers-is-loaded-for-the-devices-that-are-connected-to-20-ports"></a>2.0 ポートに接続されているデバイス用に読み込まれるドライバーのセットを教えてください。

ホストコントローラーの種類ごとに、異なるバイナリセットが読み込まれます。 Windows が読み込む USB ドライバースタックは、接続されているデバイスの速度ではなく、ホストコントローラーの種類に関連していることを理解しておくことが重要です。

このイメージでは、さまざまな種類の USB ホストコントローラーごとに読み込まれているドライバーを確認できます。

![windows 8 の usb ドライバースタック](images/usb-win8-driver-stacks.png)

USB 3.0 ポートが xHCI コントローラーに正しくルーティングされている場合、Windows は xHCI ドライバースタック (USB 3.0 ドライバースタックとも呼ばれます) を読み込みます。

Usb 2.0 ポートが USB 2.0 ハブを介して EHCI コントローラーに接続されている場合、トラフィックは EHCI コントローラーを通過し、USB 2.0 ドライバースタックが読み込まれます。

USB ドライバースタックのドライバーの詳細については、「 [Windows の usb ホスト側ドライバー](https://go.microsoft.com/fwlink/p/?linkid=320134)」を参照してください。

PC の USB 2.0 ポートでコンパニオンコントローラーが使用されている場合、ポートがルーティングされるホストコントローラーはデバイスの速度に依存します。 たとえば、低速度のデバイスは、UHCI または OHCI コントローラーを介して接続し、USBUHCI または USBOHCI ドライバーを使用します。 PC が高速デバイスを EHCI コントローラーにルーティングするため、Windows では USBEHCI ドライバーが使用されます。

デバイスの速度が異なると、コントローラー用に読み込まれているドライバーは特定されません。 ただし、デバイスの速度が異なると、使用するコントローラーが決まります。 コントローラーは常に同じドライバーを使用します。

## <a name="how-do-i-determine-whether-my-usb-30-device-is-operating-as-superspeed"></a>USB 3.0 デバイスが SuperSpeed として動作しているかどうかを判断操作方法には

Windows 8 では、まず、USB 3.0 ポートと xHCI ホストコントローラーがあることを確認します。 SuperSpeed USB デバイスが xHCI ホストコントローラーに接続されている場合は、windows 8 UI の特定の部分で "USB 3.0 に接続しています" というメッセージが表示されます。 デバイスが XHCI コントローラーではなく EHCI コントローラーに接続されている場合は、メッセージが読み取られます。 "デバイスは USB 3.0 に接続すると、高速に実行できます" と表示されます。

これらの UI メッセージは、[PC 設定] で確認できます。

1. Charms バーを開きます (カーソルを画面の上端または右下隅にドラッグするか、Windows キー + C を入力するか、指で右からスワイプします)。
2. [**設定**] を選択し、[ **PC の設定**] を変更します。
3. [ **PC 設定**] で**デバイス**を選択します。

この画像は、USB 3.0 デバイスが SuperSpeed で動作しているときの UI メッセージを示しています。

![superspeed で動作する superspeed usb デバイス ](images/usb-superspeed.jpg)

この画像は、USB デバイスが SuperSpeed より低いバス速度で動作しているときの UI メッセージを示しています。

![superspeed usb デバイスが高速に動作 ](images/usb-high-speed.jpg)

次の図に示すように、[デバイスとプリンター] で同様のメッセージを表示できます。

![superspeed で動作する superspeed usb デバイス](images/usb-superspeed-devices.jpg)

![高速で動作する superspeed デバイス](images/usb-high-speed-devices.jpg)

USB 3.0 デバイスが記憶装置の場合、次に示すように、ボリュームラベルが選択されると、エクスプローラーに類似のメッセージが表示されます。 メッセージを表示するには、**ビュー&gt; の詳細**ペインを選択する必要があることに注意してください。

![superspeed で動作する superspeed usb デバイス ](images/usb-superspeed-storage-device.jpg)

![superspeed usb デバイスが高速に動作](images/usb-high-speed-storage-device.jpg)

デバイスドライバーを作成する場合、Windows Driver Kit (WDK) に含まれている[Usbview](https://go.microsoft.com/fwlink/p/?linkid=320135)ツールは非常に便利です。 Windows 8 WDK の場合、Microsoft は USBView を更新して SuperSpeed USB 情報を表示します。 このツールを使用すると、デバイスが SuperSpeed で動作しているかどうかを判断できます。 このイメージは、SuperSpeed で動作している USB 3.0 デバイスを USBView で示しています。

![superspeed で動作する superspeed usb デバイス](images/usb-superspeed-usbview.jpg)

デバイスドライバーの開発者の場合、usb[ドライバースタック](https://go.microsoft.com/fwlink/p/?linkid=320134)は IOCTL\_usb\_と呼ばれる新しい ioctl を公開します。この ioctl は[\_ノード\_接続\_](https://go.microsoft.com/fwlink/p/?linkid=320136)\_\_V2 を取得します。これを使用して、usb 3.0 デバイスの速度情報を照会できます。

## <a name="why-isnt-my-superspeed-usb-device-faster-than-an-equivalent-high-speed-usb-device"></a>SuperSpeed USB デバイスが同等の高速 USB デバイスより高速ではないのはなぜですか。

一般に、USB 3.0 USB デバイスが高速 USB デバイスより高速ではない場合、SuperSpeed では実行されません。 SuperSpeed USB デバイスが USB 3.0 ポートに接続されている場合、次の理由により、SuperSpeed で動作しない可能性があります。

- USB 2.0 ハブを使用している。

    ハブを使用している場合は、USB 3.0 ハブであることを確認します。 USB 2.0 ハブを使用している場合は、接続されている SuperSpeed USB デバイスは高速で動作します。 ハブを USB 3.0 ハブに置き換えるか、デバイスを USB 3.0 ポートに直接接続します。

- USB 3.0 hub のファームウェアが最新ではありません。

    以前の USB 3.0 ハブは正常に機能しませんでした。 このため、Windows では、これらのハブの2.0 部分のみを使用します。 このイメージに示されているように、デバイスマネージャーが "機能していない" ハブを示している場合、Windows 8 はハブの3.0 部分を使用していません。

    ![機能していない superspeed usb ハブ](images/usb-superspeed-nonfunctional.jpg)

    SuperSpeed デバイスを USB 3.0 ポートに直接接続するか、ハブのファームウェアを更新することができます。 Windows 8 は、新しいファームウェアが搭載されているハブを認識します。

- デバイスは USB 2.0 ケーブルで接続されています。

    デバイスへの接続に使用されているケーブルが USB 3.0 ケーブルであることを確認します。 また、USB 3.0 ケーブルに信号の整合性の問題がある可能性もあります。 この場合、デバイスが高速に切り替わることがあります。 その場合は、別の USB 3.0 ケーブルを使用する必要があります。

- デバイスのファームウェアが最新ではありません。

    製造元の web サイトから最新バージョンを入手して、SuperSpeed USB デバイスのファームウェアを更新します。 一部の SuperSpeed USB デバイス製造元は、ファームウェアの更新プログラムとして、デバイスで見つかったバグの修正プログラムをリリースします。

- ホストコントローラーのファームウェアが最新ではありません。

    PC 製造元のサイトから最新のバージョンを入手するか、カードの製造元の追加のサイトから、USB 3.0 コントローラーのファームウェアを更新します。 一部の USB 3.0 コントローラー製造元では、ファームウェアの更新プログラムとして、コントローラーで見つかったバグの修正プログラムがリリースされています。

- システムの BIOS が最新ではありません。

    PC メーカーから最新バージョンを入手して、システムの BIOS を更新します。 マザーボードによっては、BIOS が xHCI ホストコントローラーに接続されているデバイスを EHCI コントローラーに誤ってルーティングすることがあります。 ルーティングが正しくないと、SuperSpeed USB デバイスは高速で動作します。 BIOS の更新により、この問題を解決できる場合があります。

## <a name="is-it-possible-to-have-a-composite-and-a-compound-device-in-one-piece-of-hardware"></a>1つのハードウェアに複合デバイスと複合デバイスを用意することはできますか。

できます。 3ポートのバスを搭載したハブを搭載した Microsoft 自然キーボード Pro は、複合複合 USB デバイスの一例です。 デバイスには、ポート1に接続された複合デバイスがあります。 2つの追加のポートがエンドユーザーに公開されます。

ポート1に接続されているデバイスは、低速の複合デバイスです。 デバイスには、2つのインターフェイスがあります。どちらも、ヒューマンインターフェイスデバイス (HID) の USB 標準デバイスクラス定義に準拠しています。 複合デバイスは、最上位レベルのコレクションを使用して、1つの HID インターフェイスですべてのコレクションを多重化するのではなく、2つの HID インターフェイスを提供します。 この設計は、旧バージョンの Bios との互換性のために選択されました。

## <a name="why-are-some-of-my-usb-devices-reinstalled-when-they-are-moved-to-a-new-port"></a>新しいポートに移動すると、USB デバイスの一部が再インストールされるのはなぜですか。

Windows 2000 以降のオペレーティングシステムでは、USB デバイスがあるポートから別のポートに移動されると、新しい物理デバイスオブジェクト (PDO) が作成されます。 ハードウェアが一意の USB シリアル番号を報告した場合、新しい PDO は作成されません。

同じ PDO を再利用し、デバイスを同じポートまたは新しいポートに再挿入するかどうかにかかわらず、デバイスのエクスペリエンスが変更されないようにするには、ハードウェアベンダーがデバイスにシリアル番号を格納する必要があります。 Windows ハードウェア認定プログラムの要件に従って、シリアル番号は、デバイスのインストール識別子を共有するすべてのデバイスで一意である必要があります。

## <a name="is-there-a-list-of-design-recommendations-for-usb-product-packaging"></a>USB 製品パッケージの設計に関する推奨事項の一覧がありますか。

USB (if) は、Microsoft および他の USB-IF メンバー企業と協力して、独立系ハードウェアベンダーがパッケージに含める推奨事項の一覧を作成しました。

詳細については、USB Web サイトを参照してください。

USB の高速および SuperSpeed については、 [https://www.usb.org/](https://www.usb.org/)を参照してください。

## <a name="do-i-have-to-rewrite-my-client-driver-to-support-usb-30-devices"></a>USB 3.0 デバイスをサポートするようにクライアントドライバーを書き換える必要がありますか。

すべての既存のクライアントドライバーは、低、完全、または高速のデバイスが USB 3.0 ポートに接続されている場合と同様に動作します。 Windows 8 では、既存のクライアントドライバーとの互換性が確保されています。

USB 3.0 ドライバースタックは、IRQL レベル、呼び出し元コンテキスト、およびエラー状態を管理します。デバイスと対話するときの再試行の頻度とタイミング、および既存のドライバーが引き続き動作することを確認します。 テストすることも非常に重要です。

一般的なエラーは次のような場合に発生します。

- SuperSpeed エンドポイントコンパニオンの記述子が存在するため、ドライバーのエンドポイント記述子の解析が中断します。
- 速度が向上するため、アプリケーションプロトコルレベルでタイミングの問題が発生する可能性があります。
- エンドポイントでサポートされる最大パケットサイズが異なる場合があります。
- 関数の電源管理により、セレクティブサスペンド操作のタイミングが異なる場合があります。

Windows 7 以前のバージョンのオペレーティングシステムでは、USB 3.0 ドライバースタックはサードパーティによって提供されています。 そのため、サードパーティの USB ドライバースタックで動作するようにドライバーをテストすることを強くお勧めします。

高速で SuperSpeed USB デバイス向けの Windows 8 の新しいクライアントドライバーでは、新しい機能を選択する必要があります。

## <a name="which-driver-is-loaded-for-my-superspeed-storage-device-use-uaspstorsys-or-usbstorsys"></a>SuperSpeed ストレージデバイスで使用されているドライバー (Uaspstor または Usbstor.sys)

USB 接続 SCSI (UAS) プロトコルは、確立された USB 大容量記憶装置プロトコル (ボット) に対してパフォーマンスを向上するように設計された新しい大容量記憶装置プロトコルです。 これは、プロトコルのオーバーヘッドを減らし、SATA ネイティブコマンドキュー (NCQ) をサポートし、複数のコマンドを並行して処理することで実現されます。 これを行うために、UA は、ストリームと呼ばれる一括転送に新しい USB 3.0 機能を使用します。

既存の大容量記憶装置ドライバー Usbstor.sys は、BOT プロトコルを使用します。 SuperSpeed USB デバイスなど、あらゆる速度のデバイスで動作します。

Windows 8 の場合、Microsoft には、UA プロトコルを使用する新しい大容量記憶装置クラスドライバー Uaspstor が付属しています。 ストリームは USB 3.0 の新機能であるため、Uaspstor は、ハードウェアでストリームがサポートされている場合にのみストリームを使用できます (SuperSpeed USB デバイスは xHCI ホストコントローラーに接続されています)。 また、ドライバーにはソフトウェアストリームのサポートも含まれているので、ホストの種類に関係なく、高速で動作するデバイスにも読み込むことができます。

大容量記憶装置を Windows 8 に接続し、そのデバイスで UA がサポートされている場合は、Windows によって Uaspstor 読み込まれます。 場合によっては、特定の xHCI ホストコントローラーのハードウェアストリームに関する既知の問題や、デバイスの UAS プロトコルの実装に関する既知の問題が考えられます。 このような場合、Windows は BOT プロトコルにフォールバックし、代わりに Usbstor.sys ドライバーを読み込みます。

Uaspstor は Windows 8 に新しく追加されたものです。 以前のバージョンの Windows には存在しません。

## <a name="which-usb-dwg-classes-does-microsoft-support"></a>Microsoft はどの USB DWG クラスをサポートしていますか。

Windows は、USB デバイスの作業グループ (DWG) によって定義されているいくつかの USB クラスをサポートしています。 現在の USB クラス仕様およびクラスコードの一覧については、 [https://www.usb.org/documents]( https://go.microsoft.com/fwlink/p/?LinkId=623332)の Usb DWG Web サイトを参照してください。

次の表は、Windows でサポートされている USB DWG クラスを示しています。また、各クラスをサポートする Windows のバージョンも示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>クラスの指定</th>
<th>bDeviceClass コード</th>
<th>ドライバー名</th>
<th>Windows のサポート</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Bluetooth クラス</td>
<td>0xE0</td>
<td>Bthusb .sys</td>
<td>Windows XP 以降</td>
</tr>
<tr class="even">
<td>チップ/スマートカードインターフェイスデバイス (CCID)</td>
<td>0x0B</td>
<td>Usbccid .sys</td>
<td><p>Windows Server 2008 以降</p>
<p>Windows Vista 以降</p>
<p>Windows Server 2003<em></p>
<p>Windows XP</em></p>
<p>Windows 2000<em></p></td>
</tr>
<tr class="odd">
<td>Hub クラス</td>
<td>0x09</td>
<td>Usbhub</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="even">
<td>ヒューマン インターフェイス デバイス (HID)</td>
<td>0x03</td>
<td>Hidusb .sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="odd">
<td>大容量記憶装置クラス (MSC)</td>
<td>0x08</td>
<td>Usbstor.sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="even">
<td>USB 接続 SCSI (UAS)</td>
<td>0x08</td>
<td>Uaspstor</td>
<td><p>Windows Server 2012</p>
<p>Windows 8</p></td>
</tr>
<tr class="odd">
<td>印刷クラス</td>
<td>0x07</td>
<td>Usbprint .sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="even">
<td>スキャン/イメージング (PTP)</td>
<td>0x06</td>
<td><p>WpdUsb .sys</p>
<p>Usbscan .sys</p></td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="odd">
<td>メディア転送 (MTP)</td>
<td>0x06</td>
<td>WpdUsb .sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p></td>
</tr>
<tr class="even">
<td>USB オーディオクラス</td>
<td>0x01</td>
<td>Usbaudio. sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="odd">
<td>Modem クラス (CDC)</td>
<td>0x02</td>
<td>Usbser</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="even">
<td>Video クラス (UVC)</td>
<td>0x0E</td>
<td>Usbvideo. sys</td>
<td><p>Windows Vista 以降</p>
<p>Windows XP</em></p></td>
</tr>
</tbody>
</table>

このドライバーはオペレーティングシステムより後にリリースされている可能性があるため、このドライバーを読み込むには \*特別な指示が必要です。 Windows クラスドライバーは、DWG クラス仕様で説明されているすべての機能をサポートしていない場合があります。 この場合、ドライバーはクラスの一致に基づいて読み込まれません。 クラス仕様内で実装されている機能の詳細については、WDK のドキュメントを参照してください。

## <a name="which-device-setup-class-should-i-use-for-a-custom-usb-device"></a>カスタム USB デバイスにどのデバイスセットアップクラスを使用する必要がありますか。

Microsoft では、ほとんどの種類のデバイスに対してシステム定義のセットアップクラスを提供しています。 システム定義のセットアップクラス Guid は、Devguid .h で定義されています。 詳細については、「WDK」を参照してください。 Windows クラス Guid の一覧については、次のトピックを参照してください。

- [ベンダーが使用できるシステム定義のデバイスセットアップクラス](https://go.microsoft.com/fwlink/p/?linkid=320141)
- [システムで使用するために予約されているシステム定義のデバイスセットアップクラス](https://go.microsoft.com/fwlink/p/?linkid=320142)

独立系ハードウェアベンダーは、バスの種類ではなく、USB デバイスの種類に関連付けられているセットアップクラスを使用する必要があります。 Microsoft によって既存のクラス GUID が提供されていないデバイスの種類を開発している場合は、新しいデバイスセットアップクラスを定義できます。

Windows 8 では、" **Usbdevice** " という名前の新しいセットアップクラスが定義されています (classguid = {88 Bae032-5a81-49F0-bc3de4ff138216d6})。 デバイスの種類を開発している場合は、セットアップクラスの**USB**ではなく、デバイスを**usbdevice**に関連付けます。 **Usbdevice**クラスは、Windows Vista 以降のバージョンのオペレーティングシステムで動作します。

セットアップクラス**usb** (classguid = {36fc9e60-c465-11cf-8056-444553540000}) は、usb ホストコントローラーと usb ハブ専用に予約されており、他のデバイスカテゴリには使用できません。 このセットアップクラスを誤って使用すると、デバイスドライバが Windows ロゴテストに失敗する可能性があります。

## <a name="why-wont-my-cpu-enter-c3-when-i-attach-some-usb-devices"></a>USB デバイスを接続したときに CPU が C3 にならないのはなぜですか。

USB デバイスが接続されている場合、USB ホストコントローラーは、ダイレクトメモリアクセス (DMA) バスマスター操作であるフレームスケジューラをポーリングします。 バスマスタトラフィック、割り込み、またはその他のいくつかのシステムアクティビティなどの "中断イベント" は、cpu を C3 から除外します。これは、cpu のキャッシュを C3 に捜索ことができないためです。

この問題を回避するには、次の2つの方法があります。

- ハードウェアの削除。

    場合によっては、ユニバーサルシリアルバスからハードウェアを電子的に切断できます。 たとえば、USB リーダーから記憶メディアを削除すると、USB リーダーは、電子切断をエミュレートし、メディアが再挿入されたときに再接続することができます。 この場合、ホストコントローラーに USB デバイスがないため、C3 の移行が発生する可能性があります。

- セレクティブサスペンド。

    Windows XP 以降のオペレーティングシステムで使用できる唯一の代替手段は、USB のセレクティブサスペンドをサポートすることです。 この機能を使用すると、システム自体が完全に動作している電源状態 (S0) にある場合でも、デバイスがアイドル状態になったときに制御する USB デバイスをドライバーで中断できます。 セレクティブサスペンドは、すべての USB 関数ドライバーがサポートしている場合は特に強力です。 1つのドライバーでもサポートされていない場合、CPU は C3 に入ることができません。 選択的中断の詳細については、「WDK」を参照してください。

## <a name="which-usb-class-drivers-support-selective-suspend"></a>セレクティブサスペンドをサポートする USB クラスドライバー

セレクティブサスペンドをサポートする Windows 8 の USB クラスドライバーの一覧を次に示します。

- [Bluetooth]

    このドライバーは、Windows XP Service Pack 2 以降のバージョンの Windows を実行しているコンピューター上のデバイスを選択的に中断できます。 ドライバーでは、Bluetooth ラジオで、構成記述子に自己給電とリモートウェイクのビットを設定する必要があります。 アクティブな Bluetooth 接続が存在しない場合、ドライバーは Bluetooth ラジオを選択的に中断 (D2) します。

- USB HID

    このドライバーは、HID デバイスを選択的に中断できます。 すべてのデバイスの状態の変更に対してリモートウェイク信号をトリガーする必要があります。 HID スタックでセレクティブサスペンドを有効にするには、デバイスの特定の VID + PID に対して SelectiveSuspendEnabled レジストリ値が有効になっている必要があります。 例については、「Input .inf」を参照してください。

    Windows 8 のコネクトスタンバイをサポートするシステムでは、このドライバーはシステムがコネクトスタンバイ状態のときにセレクティブサスペンド (D2) に入ります。 このドライバーは、システムをスリープ解除して画面をオンにすることができます。

- USB ハブ

    このドライバーは、デバイスが接続されていない場合、またはそのハブに接続されているすべてのデバイスを選択的に中断できる場合に、ルートまたは外部ハブを選択的に中断できます。

- USB モデム

    このドライバーは、アクティブなモデム接続が存在しない場合に、デバイスを選択的に中断できます。

- USB ストレージ (ボット)

    このドライバーは、Windows 8 に接続されたスタンバイをサポートするシステム上のストレージデバイスを選択的に中断 (D3) することができます。 HID と同様に、すべての Windows 8 システムでセレクティブサスペンドを有効にするためのレジストリの上書きがあります。

- USB ストレージ (UAS)

    このドライバーは、ディスクのタイムアウト期間中に記憶装置がアイドル状態になったときに、その記憶装置を選択的に中断 (D3) できます。

- USB ビデオ

    このドライバーは、Windows Vista 以降のオペレーティングシステムで、web カメラを選択的に中断 (D3) できます。

- USB オーディオ

    このドライバーは、コンピューターがバッテリ電源で動作しているときに、Windows 7 以降のオペレーティングシステム上の USB オーディオデバイスを選択的に中断 (D3) できます。

- 複合 USB

    このドライバーは、すべての子が中断状態のときに、複合デバイスを選択的に中断 (D3) できます。 D3-コールドをサポートするシステムでは、すべての子が D3-コールドを選択する必要があります。

- USB スマートカード

    このドライバーは、Windows 7 以降のオペレーティングシステムでは、既定で、スマートカードインターフェイスデバイスを選択的に中断 (D2) できます。

- 汎用 USB 周辺機器 (WinUSB)

    このドライバーは、Windows Vista 以降のオペレーティングシステムで、既定で選択的に一時停止 (D3) できます。

- WWAN: 3G または WiMax ドングル

    このドライバーは、デバイスを選択的に中断できます。 アクティブなサブスクリプションがある場合、デバイスは D2 に入ります。アクティブなサブスクリプションがない場合、デバイスは D3 に入ります。

## <a name="why-cant-a-usb-device-awaken-windows-from-s3"></a>USB デバイスが S3 から Windows を目覚めできないのはなぜですか。

USB デバイスは、次のようないくつかの理由により、S3 から Windows を目覚め解除できません。

1. BIOS が正しくありません。

    コンピューターに最新の BIOS がインストールされていることを確認します。 コンピューターの最新の BIOS リビジョンを取得するには、OEM または ODM の Web サイトにアクセスします。

2. スリープ解除が有効になっていない BIOS。

    一部の Bios では、S3 と S4 からのウェイクを無効にすることができます。 BIOS で S3 からの復帰が有効になっていることを確認します。

3. USBBIOSx レジストリキーが設定されていません。

    Windows XP のクリーンインストールには、USBBIOSx レジストリキーがありません。 BIOS が S3 からウェイクアップできることを OEM または ODM が検証した場合は、このレジストリキーを0x00 に設定し、コンピューターを再起動します。

4. ホストコントローラーの電源が S3 または S4 になっていません。

    Pc の電源が省電力状態になると、多くの場合、PC はアドインカードの電源を切ります。 アドインカードに電源が供給されていない場合は、wake イベントを検出できず、PC をスリープ解除できません。

詳細については、Windows XP 以降のバージョンの Windows のヘルプとサポートセンターにある USB トラブルシューティングを参照してください。

## <a name="do-i-need-to-install-drivers-for-my-enhanced-usb-20-host-controller"></a>Enhanced (USB 2.0) ホストコントローラーのドライバーをインストールする必要がありますか。

次のバージョンの Windows では、USB 2.0 拡張ホストコントローラーがサポートされています。

- Windows Vista 以降
- Windows Server 2003 以降
- Windows XP Service Pack 1
- Windows 2000 Service Pack 4

**注**   windows 2000 および windows XP は、USB 2.0 ハードウェアを利用できるようになる前にリリースされていたため、これらのオペレーティングシステムのドライバーはサービスパックにリリースされました。 ドライバーをインストールするには:

1. 最初の質問の答えで説明されている手順に従って、コンピューターに USB 2.0 ポートがあること、および拡張ホストコントローラー用のドライバーをインストールする必要があることを確認します。
2. [デバイスマネージャー] ウィンドウで、最初の質問で説明されているように [**その他のデバイス**] セクションを展開し、[ **Universal SERIAL Bus (USB) コントローラー**] をダブルクリックします。
3. [プロパティ] ダイアログボックスの [**全般**] タブで、[**ドライバーの再インストール**] をクリックします。

    ![ドライバーの再インストール](images/usb-reinstall-driver.jpg)

4. 新しいハードウェアの追加ウィザードで、[**ソフトウェアを自動的にインストールする (推奨)**] を選択し、[**次へ**] をクリックします。 ウィザードの最後のページが表示されるまで、すべての既定のオプションをそのまま使用してウィザードを続行し、[**完了**] をクリックします。 インストールを完了するには、コンピューターの再起動が必要になる場合があります。

**注**   コンピューターに最新の更新プログラムがインストールされていることを確認するには、Windows Update 定期的にアクセスしてください。

## <a name="can-i-disable-the-hi-speed-usb-device-plugged-into-non-hi-speed-usb-port-notice"></a>"高速ではない USB ポートに接続されている高速 USB デバイス" という通知を無効にすることはできますか。

Windows XP 以降のバージョンの Windows では、高速 USB デバイスが高速でサポートされていない USB ポートに接続されている場合、ポップアップ通知が作成されます。 デバイスから最も高速なパフォーマンスを得るには、ユーザーが通知をクリックし、画面の指示に従っている必要があります。

この通知を無効にするには、次の手順を実行します。

1. この FAQ の最初の質問で説明されているように、デバイスマネージャーを開始します。
2. [デバイスマネージャー] ウィンドウで、[**ユニバーサルシリアルバスコントローラー** ] ノードを展開します。 タイトルに "Universal" または "Open" という単語が含まれているホストコントローラーを探します。 見つかった場合は、ダブルクリックします。
3. [**プロパティ**] ダイアログボックスの [**詳細設定**] タブで、[ **USB エラーについて**の通知を表示しない] を選択します。

前の手順では、"高速ではないポートに接続された高速 USB デバイスだけでなく、すべての USB 通知を無効に**する   ます**。

## <a name="is-my-usb-20-hub-single-tt-or-multi-tt"></a>USB 2.0 ハブのシングル TT またはマルチ TT ですか。

USB 2.0 ハブは、ハブ上の下流に接続されているすべてのポートに対して1つのトランザクション変換 (TT) を持つことができます。また、ハブのダウンストリーム接続ポートごとに1つの TT を持つことができます (複数の TT)。

Usb デバイス記述子の**Bdeviceprotocol**フィールドの値と、usb インターフェイス記述子の**bdeviceprotocol**フィールドの値によって、ハブがシングル tt とマルチ tt のどちらであるかが示されます。

- 単一 TT。 **Bdeviceprotocol** = = 0x01
- マルチ TT。 **Bdeviceprotocol** = = 0x02

**Usbhub**は、この設定を使用して、マルチ tt モードまたはシングル tt モードを有効にします。 Windows XP 以降では、Usbhub は、常にマルチ TT ハブでマルチ TT モードを有効にします。 TT レイアウトの詳細については、「11.14.1.3 and 11.23.1 of the [USB 2.0 Specification](https://www.usb.org/documents)」を参照してください。

## <a name="what-characters-or-bytes-are-valid-in-a-usb-serial-number"></a>USB シリアル番号で有効な文字またはバイトは何ですか。

USB デバイス記述子の**iserialnumber**フィールドは、次のように、デバイスにシリアル番号と番号が格納されているかどうかを示します。

- **iserialnumber** = = 0X00: USB デバイスにシリアル番号がありません。
- **iserialnumber** ! = 0X00: USB デバイスにシリアル番号が付いています。 **Iserialnumber**に割り当てられた値は、シリアル番号の文字列インデックスです。

デバイスにシリアル番号がある場合、シリアル番号は、同じデバイスの各インスタンスを一意に識別する必要があります。

たとえば、2つのデバイス記述子が i**Dvendor**、 **Idproduct**、 **bcddevice**の各フィールドに同一の値を持っている場合、1つのデバイスを他のデバイスと区別するために、 **iserialnumber**フィールドが異なる必要があります。

プラグアンドプレイには、USB シリアル番号のすべてのバイトが有効である必要があります。 1バイトが無効である場合、Windows はシリアル番号を破棄し、シリアル番号がないかのようにデバイスを扱います。 次のバイト値は、USB シリアル番号には有効ではありません。

- 0x2C.
- 値が0x20 未満です。
- 値が0x7F を超えています。

**Iserialnumber**値の詳細については、「9.6.1 the [USB 2.0 Specification](https://www.usb.org/documents)」の「」セクションを参照してください。

## <a name="what-langid-is-used-in-a-string-request-on-localized-builds-of-windows"></a>Windows のローカライズされたビルドにおける文字列要求では、どのような LANGID が使用されますか。

USB デバイスは、USB デバイス記述子の iSerialNumber 化フィールドをシリアル番号の文字列インデックスに設定することによって、シリアル番号が存在することを示します。 シリアル番号を取得するために、Windows は言語識別子 (LANGID) が 0x0409 (米国英語) に設定された文字列要求を発行します。 Windows では、他の言語用にローカライズされた Windows のバージョンでも、常にこの LANGID を使用して USB シリアル番号を取得します。

## <a name="what-langid-is-used-to-extract-a-devices-serial-number"></a>デバイスのシリアル番号を抽出するために使用される LANGID

USB デバイスは、USB デバイス記述子の iSerialNumber 化フィールドをシリアル番号の文字列インデックスに設定することによって、シリアル番号が存在することを示します。 シリアル番号を取得するために、Windows は言語識別子 (LANGID) が 0x0409 (米国英語) に設定された文字列要求を発行します。 Windows では、他の言語用にローカライズされた Windows のバージョンでも、常にこの LANGID を使用して USB シリアル番号を取得します。

## <a name="what-is-the-maximum-usb-transfer-size-for-different-windows-versions"></a>さまざまな Windows バージョンの USB 転送の最大サイズはどのくらいですか。

「[さまざまなオペレーティングシステムでの USB 転送の最大サイズ」を](https://support.microsoft.com/help/832430/maximum-size-of-usb-transfers-on-various-operating-systems)参照してください。

## <a name="how-should-numbers-be-assigned-to-multiple-interfaces-on-a-composite-device"></a>複合デバイスの複数のインターフェイスに番号を割り当てる方法

Windows では、1つ目の構成で複数のインターフェイスを持つ USB デバイスを複合デバイスとして扱います。

Windows XP Service Pack 1 以前のバージョンの Windows の場合:

- インターフェイス番号は、0から始まる必要があります。
- インターフェイス番号は、連続して増加する必要があります。

Windows XP Service Pack 2 以降のバージョンの Windows では、インターフェイス番号が連続していなくても増加する必要があります。

インターフェイス番号の詳細については、「 [WINDOWS XP では、順番に番号が付けられていない複合 USB デバイスが機能](https://support.microsoft.com/help/814560)しない」を参照してください。

インターフェイスの代替設定は、すべてのバージョンの Windows で次のように割り当てる必要があります。

- インターフェイスの既定値は、常に別の設定0です。
- その他の代替設定番号は、連続して増加する必要があります。

代替設定の詳細については、「9.6.5 the [USB 2.0 Specification](https://www.usb.org/documents)」セクションを参照してください。

## <a name="what-are-the-major-restrictions-imposed-by-usbccgpsys"></a>Usbccgp によって課せられる主な制限は何ですか。

Usbccgp では、次のような複合デバイスがサポートされてい**ます。**

- Windows Me
- Windows XP
- Windows Server 2003
- Windows Vista
- Windows Server 2008

ただし、これら以降のバージョンの Windows では、複合デバイスの親ドライバーとして**Usbhub**を読み込むこともできますが、ハードウェアの互換性エラーが発生する可能性があるため、Microsoft では推奨されません。 代わりに**Usbccgp**を使用してください。

複合デバイス用の正しいドライバーを確実に読み込むには、次のように、INF ファイルで Include ディレクティブと必要なディレクティブを使用します。

``` syntax
Include = USB.INF
Needs = Composite.Dev
```

**Usbccgp**によってハードウェアデバイスとドライバーに課せられる主な制限は次のとおりです。

- Usbccgp でサポートされるのは、既定の構成である configuration 0 だけです。
- Usbccgp は、Windows XP および Windows Server 2003 のセレクティブサスペンドをサポートしていません。 この機能は、Windows Vista 以降のバージョンの Windows でのみサポートされています。
    **注**   Usbccgp は、WINDOWS xp SP1 以降のバージョンの windows xp でのセレクティブサスペンドをサポートしていますが、機能が制限されています。 これらのバージョンの Windows では、デバイスの各子関数に保留中のアイドル状態の IRP がある場合にのみ、複合デバイスがセレクティブサスペンドに配置されます。 Usbccgp は、Windows XP RTM でのセレクティブサスペンドをサポートしていません。

- Usbccgp は、windows XP SP2、Windows Server 2003 SP1、およびそれ以降のバージョンの Windows でのみインターフェイスアソシエーション記述子 (IAD) をサポートしています。
- Usbccgp は、windows XP SP2、Windows Server 2003 SP1、およびそれ以降のバージョンの Windows でのみ連続しないインターフェイス番号をサポートしています。

## <a name="how-do-i-enable-debug-tracing-for-usb-core-binaries"></a>USB コアバイナリのデバッグトレースを有効に操作方法ますか?

[WPP トレースメッセージをドライバーのパブリック PDB ファイルに追加して表示する方法](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/06/29/wpp-blog-post.aspx)については、ブログの投稿を参照してください。

USB コアスタックのデバッグの詳細については、「[さまざまなドライバーおよびサブシステムで詳細デバッグトレースを有効にする方法](https://support.microsoft.com/help/314743)」を参照してください。

## <a name="does-windows-support-interface-association-descriptors"></a>Windows はインターフェイスの関連付け記述子をサポートしていますか。

できます。 USB 2.0 インターフェイスアソシエーション記述子 (IAD) エンジニアリングの変更通知 (ECN) では、インターフェイスのグループ化とその代替設定を関数内で記述するための新しい標準メソッドが導入されました。 IAD を使用すると、1つの関数内で2つ以上の連続するインターフェイスと代替設定を識別できます。

Microsoft は現在、Ihv と協力して、IAD をサポートするデバイスを開発しています。 次のオペレーティングシステムでは、IAD がサポートされています。

- Windows XP Service Pack 2 以降
- Windows Server 2003 Service Pack 1 以降
- Windows Vista

## <a name="does-the-usb-stack-handle-chained-mdls-in-a-urb"></a>USB スタックはチェーンされた MDLs を URB に処理しますか。

この機能は、Windows に付属している USB 3.0 ドライバースタックでサポートされています。

## <a name="can-a-driver-have-more-than-one-urb-in-an-irp"></a>ドライバーが1つの IRP に複数の URB を持つことはできますか。

いいえ。 この機能は、Windows に付属している USB スタックではサポートされていません。

## <a name="does-windows-support-usb-composite-hubs"></a>Windows では USB 複合ハブがサポートされるのですか。

複合 USB デバイス (多機能 USB デバイスとも呼ばれます) は複数の機能を公開し、それぞれを独立したデバイスとして扱うことができます。 システムは、デバイスの機能の eaech の親ドライバーとして機能するように、USB 汎用親ドライバー **Usbccgp**を読み込みます。 USB 汎用親ドライバーは、複合デバイスの機能を個別の USB デバイスとして列挙し、PDO を作成して、各関数のデバイススタックを構築します。

複合 USB デバイスは、ハブとして機能する関数を公開できません。 Windows では、このようなハブが正しく列挙されず、デバイスをインストールしようとするとシステムがクラッシュする可能性があります。

## <a name="related-topics"></a>関連トピック

[すべての開発者のための USB の概念](usb-concepts-for-all-developers.md)  
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  

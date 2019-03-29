---
Description: This topic presents frequently asked questions for driver developers who are new to developing and integrating USB devices and drivers with Windows operating systems.
title: Windows における USB- よくあるご質問
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90e5ffd611ce4f41f4c575defff6bd3fc5531d53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581139"
---
# <a name="usb-in-windows---faq"></a>Windows における USB- よくあるご質問


このトピックでは、初心者の開発と Windows オペレーティング システムとの USB デバイスとドライバーの統合にはドライバー開発者向けのよく寄せられる質問を表示します。

-   [質問すると、たくさんの USB 用語が聞こえます。これらすべては一体何でしょうか。](#usbterms)
-   [自分の PC に USB 3.0 ポートがあるでしょうか。](#pc-3-ports)
-   [EXtensible ホスト コント ローラー用ドライバーをインストールする必要がありますか。](#ext-drivers)
-   [私のシステムで複数のホスト コント ローラーが参照する理由](#hosts)
-   [1 つだけの USB 3.0 ハブを接続していないときに 2 つのハブ デバイス マネージャーにするはなぜですか。](#twohubs)
-   [2.0 ポートに接続されているデバイスにどのドライバー セットが読み込まれますか。](#portdrivers)
-   [USB 3.0 デバイスが SuperSpeed として動作しているかどうかを判断する方法](#superspeed)
-   [なぜ私の SuperSpeed USB デバイスを同等の高速 USB デバイスより速くないでしょうか。](#whynotfaster)
-   [複合と 1 つのハードウェアに複合デバイスを用意することはできますか。](#compositecompound)
-   [一部の USB デバイスを新しいポートに移動したときに再インストールはなぜですか。](#why-reinstalled)
-   [USB 製品パッケージのデザイン推奨一覧はありますか。](#designrec)
-   [USB 3.0 デバイスをサポートするために、クライアント ドライバーを書き直す必要はでしょうか。](#rewritedriver)
-   [SuperSpeed ストレージ デバイスで使用する、Uaspstor.sys と Usbstor.sys ドライバーが読み込まれますか。](#loadeddriver)
-   [Microsoft はどの USB DWG クラスをサポートしますか。](#usbdwg)
-   [どのデバイス セットアップ クラス、カスタムの USB デバイスを使用する必要がありますか。](#customclass)
-   [なぜしない CPU が c3 一部の USB デバイスを接続したときか。](#cpucthree)
-   [どの USB クラス ドライバーがセレクティブ サスペンドをサポートしますか。](#selsuspend)
-   [なぜことはできません、USB デバイスがスリープ解除 Windows S3 からでしょうか。](#usbawake)
-   [拡張 (USB 2.0) ホスト コント ローラー用ドライバーをインストールする必要がありますか。](#enhdriver)
-   [「高速 USB デバイスは非 HI-SPEED USB ポートに接続されている」通知を無効にできますか。](#disablehi)
-   [自分の USB 2.0 ハブ シングル TT またはマルチ TT ですか。](#singlett)
-   [どのような文字またはバイトは、USB シリアル番号で有効ですか。](#usbsn)
-   [どのような LANGID が Windows のローカライズされたビルド文字列の要求で使用されるでしょうか。](#langidloc)
-   [どのような LANGID はデバイスのシリアル番号を抽出するために使用しますか?](#langidsn)
-   [さまざまな Windows バージョンの最大の USB 転送サイズとは何ですか。](#maxxfer)
-   [番号は、複合デバイスに複数のインターフェイスにどのように割り当てする必要がありますか。](#nummultif)
-   [Usbccgp.sys によって課される主要な制約とは](#usbccgp)
-   [USB の主要なバイナリのデバッグ トレースを有効にする方法](#tracecorebin)
-   [Windows は、インターフェイスの関連付けの記述子をサポートしますか。](#iadesc)
-   [USB スタックのハンドルは、URB で MDLs チェーンされているか。](#mdlsinurb)
-   [ドライバーは IRP の 1 つ以上の URB を持つことができますか。](#urbirp)
-   [Windows は、複合の USB ハブをサポートしますか。](#supportcomposite)
-   [USB の他の Faq はどこで入手できますか。](#addlfaq)

## <a name="i-hear-numerous-usb-terms-thrown-around-almost-interchangeably-what-do-they-all-mean"></a>質問すると、たくさんの USB 用語が聞こえます。 これらすべては一体何でしょうか。


*「USB 3.0 に協力してくれたことができます、SuperSpeed USB サム ドライブを PC の xHCI ホスト コント ローラーに接続し、ファイルのコピーを高速化します。」*

前の文の USB 用語を理解しましょう。 USB 3.0、USB 2.0、および USB 1.0 は、USB 仕様のリビジョン番号を参照してください、 [USB Implementers Forum](http://www.usb.org/home)します。 USB 仕様では、どのホスト PC と USB デバイス相互に通信を定義します。

バージョン番号は、最大転送速度も示します。 仕様の最新リビジョンは、USB 3.0 では、最大転送速度は 5 Gbps を指定します。 USB 1.0 は、2 つの異なるデータ レート、低速 USB (最大 1.5 Mbps) とフル_スピード USB (最大 12 Mbps) を定義します。 USB 2.0 定義の新しいデータ速度として高速 USB (480 Mbps) 低とフル スピード デバイスのサポートを維持しながらします。 USB 3.0 は、すべての定義済みのデータ レートを使用するが続行されます。 製品のパッケージを見ると、SuperSpeed USB は最新の USB 3.0 デバイスを参照します。 高速 USB は高速 USB 2.0 デバイスを記述するために使用します。 USB、記述のないは、低速とフル_スピードのデバイスを指します。

USB プロトコルに加えて、USB ホスト コント ローラー、1 つのデバイスが接続されている PC のハードウェアの 2 番目の指定があります。 ホスト コント ローラー インターフェイス仕様では、ホスト コント ローラーのハードウェアとソフトウェアの対話方法を定義します。 EXtensible ホスト コント ローラー インターフェイス (xHCI) は、USB 3.0 ホスト コント ローラーを定義します。 エンハンス ホスト コント ローラー インターフェイス (EHCI) は、USB 2.0 ホスト コント ローラーを定義します。 ユニバーサル ホスト コント ローラー (UHCI) とオープン ホスト コント ローラー (OHCI) は 2 つ、別の USB 1.0 ホスト コント ローラーの実装。

## <a name="does-my-pc-have-usb-30-ports"></a>自分の PC に USB 3.0 ポートがあるでしょうか。


USB 3.0 ポートが、SuperSpeed USB ロゴでマークされたか、またはポートは通常は青色です。

![ロゴの usb ポート](images/usb-intro-faq-fig1-usblogo.png)

![青色の usb 3.0 ポート](images/usb-intro-faq-fig2-blueusbport.png)

新しい Pc には、USB 3.0 と USB 2.0 ポートがあります。 SuperSpeed USB デバイスを最高速度で実行する場合は、USB 3.0 ポートを検索し、デバイスをそのポートに接続します。 SuperSpeed デバイスには、USB 2.0 ポートが接続されている高速で動作します。

特定のポートが USB 3.0 ポート デバイス マネージャーでも確認することができます。 Windows Vista またはそれ以降のバージョンの Windows では、デバイス マネージャーを開きし、一覧から、ポートを選択します。

![デバイス マネージャーで usb ホスト コント ローラー](images/usb-host-controllers-dm.png)

EXtensible ホスト コント ローラーを使っている場合は、USB 3.0 をサポートします。

## <a name="do-i-need-to-install-drivers-for-my-extensible-host-controller"></a>EXtensible ホスト コント ローラー用ドライバーをインストールする必要がありますか。


Windows 8 および Windows Server 2012 には、USB 3.0 のサポートが含まれます。

PC が USB 3.0 ポートが、Windows 8 より前のバージョンの Windows を実行している場合は、ホスト コント ローラーのドライバーは、PC の製造元によって提供されます。 これらのドライバーを再インストールする必要がある場合は、製造元から入手する必要があります。

Windows 8 より前のバージョンの Windows を実行している PC に USB 3.0 コント ローラー カードを追加した場合は、コント ローラー カードの製造元によって提供されるドライバーをインストールする必要があります。

Windows 8 では、Microsoft から提供された一連の USB 3.0 ドライバー (USB ドライバー スタック) はほとんどのホスト コント ローラーを使用します。 Microsoft USB 3.0 ドライバー スタックは Fresco Logic FL1000 コント ローラーでは機能しません。 FL1000 コント ローラーがあるかどうかを決定するには、デバイス マネージャーを開くし、展開**ユニバーサル シリアル バス コント ローラー**します。 コント ローラーのノードを右クリックして、コント ローラーのプロパティを表示します。 **詳細**] タブで [**ハードウェア Id**リスト内のプロパティ。 ハードウェア ID が PCI で始まる場合\\VEN\_1B73 & DEV\_1000、FL1000 です。 そのコント ローラーをダウンロードして、PC またはコント ローラー カードの製造元からドライバーをインストールします。

## <a name="why-do-i-see-several-host-controllers-on-my-system"></a>私のシステムで複数のホスト コント ローラーが参照する理由


お使いの PC に接続する USB デバイスだけでなく、web カメラ、指紋リーダー、SD カード リーダーなど、USB 経由で接続されている PC 内で統合されたデバイス数があります。 これらのデバイスのすべての接続を外部 USB ポートを引き続き提供は、PC には、いくつかの USB ホスト コント ローラーがサポートしています。

USB 3.0 xHCI ホスト コント ローラーはすべて USB デバイスの速度、SuperSpeed、高速、フル_スピードと低速で完全に下位互換性があります。 XHCI コント ローラーに直接すべてのデバイスを接続し、そのデバイスを職場に予想されることができます。 EHCI コント ローラーでない場合。 USB 2.0 仕様には、あらゆる速度のデバイスがサポートされますが、EHCI コント ローラーは高速 USB デバイスのみをサポートします。 作業のフル_スピードと低速の USB デバイスの順序で、USB 2.0 ハブを介して EHCI コント ローラーに接続する必要があります。 または UHCI または OHCI コント ローラーに接続する必要があります。

新しい Pc、Pc によって公開されているほとんどの USB 2.0 ポートは USB 2.0 ハブのダウン ストリームです。 このハブは EHCI コント ローラーに接続されます。 これにより、あらゆる速度のデバイスを使用する PC の USB 2.0 ポートができます。 SuperSpeed デバイスは、2.0 ポートに接続されているときに、高速デバイスとして動作します。

USB 2.0 仕様がリリースされた後、Pc は、あらゆる速度のデバイスをサポートするためにホスト コント ローラーの組み合わせを使用します。 1 つの USB 2.0 ポートは、2 つのホスト コント ローラー、EHCI ホスト コント ローラーと、UHCI または OHCI ホスト コント ローラーにワイヤード (有線) なります。 デバイスを接続するときに、ハードウェアは、接続を動的に 2 つのホストのいずれかにルーティングします。 ルーチンは、デバイスの速度に依存します。

## <a name="why-do-i-see-two-hubs-in-device-manager-when-i-have-connected-only-one-usb-30-hub"></a>1 つだけの USB 3.0 ハブを接続していないときに 2 つのハブ デバイス マネージャーにするはなぜですか。


XHCI ホスト コント ローラーはどの速度のデバイスを操作するときに、SuperSpeed ハブは SuperSpeed デバイスでのみ機能します。 USB 3.0 ハブはあらゆる速度に使えるように、2 つの部分がある: SuperSpeed ハブと USB 2.0 ハブ。 USB 3.0 ハブは、によって動的にルーティング デバイス、SuperSpeed ハブまたは 2.0 ハブにデバイスの速度に基づいて、すべての速度をサポートできます。

デバイス マネージャーを開き、表示**接続によってデバイス**、eXtensible ホスト コント ローラーを見つけます。 1 つの USB 3.0 ハブを USB 3.0 ポートに接続するときに、コント ローラーのルート ハブの 2 つのハブをダウン ストリーム。

![デバイス マネージャーの usb 3.0 ハブ](images/usb-3-hub-dm.png)

次の例で、SuperSpeed USB ストレージ デバイスと USB オーディオ デバイスが両方に接続して、USB 3.0 ハブ。 ストレージ デバイスが SuperSpeed ハブのダウン ストリームとオーディオ デバイスが USB 2.0 ハブのダウン ストリームを確認できます。

![デバイス マネージャーに接続されたデバイスの usb 3.0 ハブ](images/usb-3-hub-connected-devices-dm.png)

## <a name="which-set-of-drivers-is-loaded-for-the-devices-that-are-connected-to-20-ports"></a>2.0 ポートに接続されているデバイスにどのドライバー セットが読み込まれますか。


ホスト コント ローラーの種類ごとに異なるバイナリのセットが読み込まれます。 Windows が読み込む USB ドライバー スタックが接続されているデバイスの速度が、ホスト コント ローラーの種類に関連していることを理解しておく必要があります。

この図では、どのドライバーが読み込まれる各 USB ホスト コント ローラーのさまざまな種類がわかります。

![windows 8 における usb ドライバー スタック](images/usb-win8-driver-stacks.png)

USB 3.0 ポートが xHCI コント ローラーに正しくルーティングされて、Windows は xHCI ドライバー スタック (USB 3.0 ドライバー スタックとも呼ばれます) を読み込みます。

USB 2.0 ポートが USB 2.0 ハブを介して EHCI コント ローラーに接続されている場合は、トラフィックは EHCI コント ローラーを移動され、USB 2.0 ドライバー スタックが読み込まれます。

USB ドライバー スタックのドライバーの詳細については、次を参照してください。 [Windows での USB ホスト側ドライバー](https://go.microsoft.com/fwlink/p/?linkid=320134)します。

PC の USB 2.0 ポートがコンパニオン コント ローラーを使用する場合、ポートがルーティング ホスト コント ローラーは、デバイスの速度によって異なります。 たとえば、低速デバイスは UHCI または OHCI コント ローラーを経由して接続し、USBUHCI または USBOHCI ドライバーを使用します。 PC 高速デバイスを EHCI コント ローラーにルーティングする、そのため、Windows は USBEHCI ドライバーを使用します。

別のデバイスの速度は、コント ローラーに読み込まれるドライバーを特定できません。 ただし、別のデバイスの速度は、コント ローラーの使用を判断する可能性があります。 コント ローラーは、常に同じドライバーを使用します。

## <a name="how-do-i-determine-whether-my-usb-30-device-is-operating-as-superspeed"></a>USB 3.0 デバイスが SuperSpeed として動作しているかどうかを判断する方法


Windows 8 で最初に、USB 3.0 ポートと xHCI ホスト コント ローラーがあることを確認します。 SuperSpeed USB デバイスが xHCI ホスト コント ローラーに接続されている場合、Windows 8 では、Windows 8 の UI の特定の部分での「USB 3.0 への接続済み」のメッセージが表示されます。 デバイスが XHCI コント ローラーではなく EHCI コント ローラーに接続されている場合、メッセージは代わりに読み取り、「USB 3.0 に接続されている場合に、デバイスが高速実行できます」。

PC 設定では、これらの UI メッセージを表示できます。

1.  チャーム バーを開きます (上または下の画面の右下隅にカーソルをドラッグして、Windows キー + C を入力するか、指で右からスワイプして)。
2.  選択**設定**し**PC 設定の変更**します。
3.  選択、**デバイス** **PC 設定**します。

このイメージは、USB 3.0 デバイスが SuperSpeed で動作しているときに、UI のメッセージを示します。

![superspeed usb デバイスが superspeed で ](images/usb-superspeed.jpg)

このイメージは、USB デバイスが SuperSpeed よりも小さいバス速度で動作しているときに、UI のメッセージを示します。

![高速で動作している superspeed usb デバイス ](images/usb-high-speed.jpg)

デバイスとプリンターのようなメッセージを表示するには、これらの画像に示すようにします。

![superspeed usb デバイスが superspeed で](images/usb-superspeed-devices.jpg)

![高速で動作している superspeed デバイス](images/usb-high-speed-devices.jpg)

USB 3.0 デバイスがストレージ デバイスの場合は、Windows エクスプ ローラーに表示のようなメッセージ ボリューム ラベルを選択すると、次のようです。 なお、**ビュー -&gt;詳細**メッセージを表示するウィンドウを選択してください。

![superspeed usb デバイスが superspeed で ](images/usb-superspeed-storage-device.jpg)

![高速で動作している superspeed usb デバイス](images/usb-high-speed-storage-device.jpg)

デバイス ドライバーを作成する場合、 [USBView](https://go.microsoft.com/fwlink/p/?linkid=320135) Windows Driver Kit (WDK) に含まれるツールは非常に便利です。 Windows 8 WDK の SuperSpeed USB 情報を表示する USBView が更新されます。 このツールを使用すると、デバイスが SuperSpeed で動作しているかどうかを判断します。 このイメージは、USB 3.0 デバイスが superspeed で USBView を示しています。

![superspeed usb デバイスが superspeed で](images/usb-superspeed-usbview.jpg)

デバイス ドライバー開発者は、使用する場合、 [USB ドライバー スタック](https://go.microsoft.com/fwlink/p/?linkid=320134)はという新しい ioctl [IOCTL\_USB\_取得\_ノード\_接続\_情報\_EX\_V2](https://go.microsoft.com/fwlink/p/?linkid=320136)、USB 3.0 デバイスの速度情報のクエリに使用できます。

## <a name="why-isnt-my-superspeed-usb-device-faster-than-an-equivalent-high-speed-usb-device"></a>なぜ私の SuperSpeed USB デバイスを同等の高速 USB デバイスより速くないでしょうか。


一般に、USB 3.0 の USB デバイスが高速 USB デバイスより速くがない場合、SuperSpeed で実行とはしません。 SuperSpeed USB デバイスが USB 3.0 ポートに接続されている場合に、動作しない可能性 SuperSpeed で、次の理由。

-   USB 2.0 ハブを使用しています。

    ハブを使用している場合は、USB 3.0 ハブはあることを確認します。 USB 2.0 ハブを使用している場合、接続している SuperSpeed USB デバイスは高速で動作します。 ハブ、USB 3.0 ハブと交換またはデバイスを直接 USB 3.0 ポートに接続します。

-   USB 3.0 ハブのファームウェアが古くなっています。

    特定の以前の USB 3.0 ハブはうまく機能しませんでした。 その結果、Windows は、それらのハブの 2.0 の機能のみを使用します。 デバイス マネージャーでは、この図のように、「機能不可」のハブが示されている場合は Windows 8 は、ハブの 3.0 の機能を使用していません。

    ![機能不可の superspeed usb ハブ](images/usb-superspeed-nonfunctional.jpg)

    SuperSpeed デバイスを USB 3.0 ポートに直接接続するか、ハブ上のファームウェアを更新します。 Windows 8 では、新しいファームウェアのハブを認識します。

-   デバイスが USB 2.0 ケーブルで接続します。

    デバイスの接続に使用されているケーブルが USB 3.0 ケーブルであることを確認します。 USB 3.0 ケーブルにシグナル インテグリティの問題があることもできます。 その場合は、デバイスは、高速に切り替わる可能性があります。 その場合は、別の USB 3.0 ケーブルを使用する必要があります。

-   デバイスのファームウェアが古くなっています。

    製造元の web サイトから最新バージョンを入手して SuperSpeed USB デバイスのファームウェアを更新します。 一部の SuperSpeed USB デバイス製造元では、ファームウェアの更新プログラムとして、デバイスで見つかったバグの修正プログラムをリリースします。

-   ホスト コント ローラーのファームウェアが古くなっています。

    PC の製造元のサイトからもから最新バージョンを取得することで、USB 3.0 コント ローラーのファームウェアを更新、カードの製造元のサイトに追加します。 一部の USB 3.0 コント ローラー製造元では、ファームウェアの更新プログラムとして、コント ローラーで見つかったバグの修正プログラムをリリースします。

-   システムの BIOS が古くなっています。

    PC メーカーから最新バージョンを取得することにより、システムの BIOS を更新します。 一部のマザーボードで BIOS 正しくルーティングできますない EHCI コント ローラーに xHCI ホスト コント ローラーに接続されているデバイス。 SuperSpeed USB デバイスが高速で動作するを強制ルーティングの間違いです。 BIOS の更新プログラムは、この問題を修正できます。

## <a name="is-it-possible-to-have-a-composite-and-a-compound-device-in-one-piece-of-hardware"></a>複合と 1 つのハードウェアに複合デバイスを用意することはできますか。


[はい]。 コンパウンド複合 USB デバイスの例は、Microsoft Natural Keyboard Pro が 3 つのポート、バスを利用したハブのです。 デバイスでは、ポート 1 に接続されている複合デバイスがあります。 2 つのポートは、エンドユーザーに公開されます。

ポート 1 に接続されているデバイスは、低速複合デバイスです。 デバイスでは、ヒューマン インターフェイス デバイス (HID) の USB 規格デバイス クラス定義に準拠する、2 つのインターフェイスがあります。 複合デバイスは、最上位のコレクションを使用して、1 つの HID インターフェイス経由ですべてのコレクションを多重化ではなく 2 つの HID インターフェイスを提供します。 この設計は、古い Bios と互換性のために選択されました。

## <a name="why-are-some-of-my-usb-devices-reinstalled-when-they-are-moved-to-a-new-port"></a>一部の USB デバイスを新しいポートに移動したときに再インストールはなぜですか。


Windows 2000 および以降のオペレーティング システムでは、USB デバイスが別の 1 つのポートに移動した場合は、新しい物理デバイス オブジェクト (PDO) が作成されます。 ハードウェア固有の USB シリアル番号を報告する場合は、新しい PDO は作成されません。

同じ PDO を再利用して、デバイス エクスペリエンス変更されていないこと、デバイスが同じポートでも新しいポートに再度挿入されるかどうかを確認するには、ハードウェア ベンダーは自身のデバイスでシリアル番号を格納する必要があります。 Windows ハードウェア認定プログラムの要件に従ってシリアル番号はデバイスのインストール id を共有するすべてのデバイスに対して一意である必要があります。

## <a name="is-there-a-list-of-design-recommendations-for-usb-product-packaging"></a>USB 製品パッケージのデザイン推奨一覧はありますか。


USB の場合は、Microsoft およびその他の USB と協力して-独立系ハードウェア ベンダーが、パッケージに含めるための推奨事項の一覧を作成する場合はメンバー企業です。

詳細については、USB Web サイトで使用できます。

USB および高速 USB を参照してください: [ http://www.usb.org/developers/packaging ](http://www.usb.org/developers/packaging/)/。

SuperSpeed USB を参照してください:<http://www.usb.org/channel/>します。

## <a name="do-i-have-to-rewrite-my-client-driver-to-support-usb-30-devices"></a>USB 3.0 デバイスをサポートするために、クライアント ドライバーを書き直す必要はでしょうか。


既存のすべてのクライアント ドライバーは、低、いっぱいの場合は、作業を続行するか、高速のデバイスが USB 3.0 ポートに接続されています。 Windows 8 では、既存のクライアント ドライバーとの互換性を確認されています。

USB 3.0 ドライバー スタック IRQL レベル、呼び出し元コンテキスト、およびエラーの状態を維持します。デバイス、および既存のドライバーが作業を続けるように対話するときに、頻度とタイミングを再試行してください。 テストする非常に重要ですが。

一般的なエラーが発生します。

-   ドライバーのエンドポイント記述子が SuperSpeed エンドポイント コンパニオンの記述子の存在によって改行を解析します。
-   速度の向上により、アプリケーション プロトコル レベルでタイミングの問題に実行する場合があります。
-   エンドポイントでサポートされている最大パケット サイズが異なる可能性があります。
-   \\タイミングの機能の電源管理のため選択的な中断操作が異なる可能性があります。

Windows 7 と以前のバージョンのオペレーティング システムでは、USB 3.0 ドライバー スタックは、サード パーティによって提供されます。 そのため、サード パーティ製の USB ドライバー スタックを使用するドライバーをテストすることを強くお勧めします。

高速および SuperSpeed USB デバイスを Windows 8 でのクライアント ドライバーは新しいの新機能を選択する必要があります。

## <a name="which-driver-is-loaded-for-my-superspeed-storage-device-use-uaspstorsys-or-usbstorsys"></a>SuperSpeed ストレージ デバイスで使用する、Uaspstor.sys と Usbstor.sys ドライバーが読み込まれますか。


USB 接続 SCSI (UAS) プロトコルは、一括専用 Transport (BOT) 確立された USB マス ストレージ プロトコル経由でパフォーマンスを向上させるために設計されています新しいマス ストレージ プロトコルです。 これは SATA ネイティブ コマンド キューイング (NCQ) をサポートしているプロトコルのオーバーヘッドを減らすことで、複数のコマンドを並列で処理することによって。 これを行うには、UA は、USB 3.0 の新しい機能をバルク転送と呼ばれるストリーム。

既存のマス ストレージ ドライバー Usbstor.sys、BOT プロトコルを使用します。 SuperSpeed USB デバイスを含め、デバイスのすべての速度で動作します。

Windows 8 では、新しい大容量記憶装置クラス ドライバー Uaspstor.sys UAS プロトコルを使用しています。 ストリームは USB 3.0 に新しいため、そのため Uaspstor.sys のみ使用できますストリーム ハードウェア (SuperSpeed USB デバイスが xHCI ホスト コント ローラーに接続されている) ストリームをサポートしている場合。 ドライバーもサポートしています、ソフトウェア ストリームのため、デバイスで読み込むことができますもホストの種類に関係なく、高速です。

大容量記憶装置デバイスを Windows 8 に接続するであり、そのデバイスが UAS をサポートする場合、Windows は、Uaspstor.sys を読み込みます。 場合によってである可能性がありますが認識またはデバイスの UAS プロトコルの実装に関する既知の問題の特定の xHCI ホスト コント ローラー上のハードウェア ストリームで問題。 ような場合は、Windows は、BOT プロトコルにフォールバックし、代わりに Usbstor.sys ドライバーを読み込みます。

Uaspstor.sys は Windows 8 で新しく導入します。 以前のバージョンの Windows に存在するがありません。

## <a name="which-usb-dwg-classes-does-microsoft-support"></a>Microsoft はどの USB DWG クラスをサポートしますか。


Windows では、USB デバイス Working Group (DWG) が定義されているいくつかの USB クラスをサポートします。 USB クラス仕様とクラス コードの現在の一覧については、USB DWG Web サイトを参照してください。 [ http://www.usb.org/developers/devclass\_docs]( https://go.microsoft.com/fwlink/p/?LinkId=623332)します。

このテーブルは、Windows でサポートされている USB DWG クラスを強調表示し、また各クラスをサポートする Windows のバージョンを示します。

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
<td>Bthusb.sys</td>
<td>Windows XP 以降</td>
</tr>
<tr class="even">
<td>チップ/スマート カード インターフェイス デバイス (CCID)</td>
<td>0x0B</td>
<td>Usbccid.sys</td>
<td><p>Windows Server 2008 以降</p>
<p>Windows Vista 以降</p>
<p>Windows Server 2003<em></p>
<p>Windows XP</em></p>
<p>Windows 2000<em></p></td>
</tr>
<tr class="odd">
<td>Hub クラス</td>
<td>0x09</td>
<td>Usbhub.sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="even">
<td>ヒューマン インターフェイス デバイス (HID)</td>
<td>0x03</td>
<td>Hidusb.sys</td>
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
<td>Uaspstor.sys</td>
<td><p>Windows Server 2012</p>
<p>Windows 8</p></td>
</tr>
<tr class="odd">
<td>印刷クラス</td>
<td>0x07</td>
<td>Usbprint.sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="even">
<td>スキャン/イメージング (PTP)</td>
<td>0x06</td>
<td><p>WpdUsb.sys</p>
<p>Usbscan.sys</p></td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="odd">
<td>メディア転送 (MTP)</td>
<td>0x06</td>
<td>WpdUsb.sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p></td>
</tr>
<tr class="even">
<td>USB オーディオ クラス</td>
<td>0x01</td>
<td>Usbaudio.sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="odd">
<td>モデム クラス (CDC)</td>
<td>0x02</td>
<td>Usbser.sys</td>
<td><p>Windows Server 2003 以降</p>
<p>Windows XP 以降</p>
<p>Windows 2000 以降</p></td>
</tr>
<tr class="even">
<td>ビデオ クラス (UVC)</td>
<td>0x0E</td>
<td>Usbvideo.sys</td>
<td><p>Windows Vista 以降</p>
<p>Windows XP</em></p></td>
</tr>
</tbody>
</table>

 

\*特別な手順については、このドライバーがリリースされたオペレーティング システムよりも後であるために、このドライバーを読み込むために必要です。 Windows クラス ドライバーが可能性があります DWG クラス仕様で説明されている機能のすべてをサポートしていません。 この場合、ドライバーはクラスの一致に基づいて読み込みません。 クラス仕様の中で実装された機能については、WDK のマニュアルを参照してください。

## <a name="which-device-setup-class-should-i-use-for-a-custom-usb-device"></a>どのデバイス セットアップ クラス、カスタムの USB デバイスを使用する必要がありますか。


Microsoft では、ほとんどのデバイスの種類のシステム定義のセットアップ クラスを提供します。 システム定義のセットアップ クラス Guid は Devguid.h で定義されます。 詳細については、WDK を参照してください。 クラス Guid の Windows の一覧については、これらのトピックを参照してください。

-   [システム定義のデバイス セットアップ クラスがベンダーに使用できます。](https://go.microsoft.com/fwlink/p/?linkid=320141)
-   [システム定義のデバイス セットアップ クラスがシステム用に予約されています](https://go.microsoft.com/fwlink/p/?linkid=320142)

独立系ハードウェア ベンダーは、バスの種類ではなく、USB デバイスの種類に関連付けられているセットアップ クラスを使用する必要があります。 デバイスの種類を Microsoft が指定されていない既存のクラス GUID を開発している場合は、新しいデバイス セットアップ クラスを定義できます。

Windows 8 では、新しいセットアップ クラスが定義されて、名前付き**USBDevice** (ClassGuid = {88bae032-5a81-49f0-bc3d-a4ff138216d6})。 デバイスの種類を開発している場合を使用してデバイスを関連付ける**USBDevice**セットアップ クラスではなく**USB**します。 **USBDevice**クラスは、Windows Vista およびそれ以降のバージョンのオペレーティング システムで動作します。

セットアップ クラス**USB** (ClassGuid = 36fc9e60-c465-11cf-8056-444553540000) は USB ホスト コント ローラーと USB ハブに対してのみに予約されており、他のデバイス カテゴリは使用しないでください。 このセットアップ クラスを正しく使用すると、各デバイス ドライバーが Windows ロゴ テストに失敗する可能性があります。

## <a name="why-wont-my-cpu-enter-c3-when-i-attach-some-usb-devices"></a>なぜしない CPU が c3 一部の USB デバイスを接続したときか。


USB デバイスが接続されると、USB ホスト コント ローラーは、ダイレクト メモリ アクセス (DMA) バス マスター操作にはフレーム スケジューラをポーリングします。 「中断イベント」など、バス マスター トラフィック、割り込み、またはその他のシステム アクティビティがいくつかあるため、定義上、C3 では、CPU のキャッシュは覗き見ことはできません、CPU が C3 の外に移動します。

この問題を回避する 2 つの方法はあります。

-   ハードウェアの削除。

    ハードウェアをユニバーサル シリアル バスから電子的に切断できます。 たとえば、USB リーダーから削除されると、記憶域メディアに、USB リーダーが、電子的な切断をエミュレートおよびメディアが再度挿入されるときに再接続することができます。 この場合、ホスト コント ローラー上の USB デバイスがないため、C3 に移行が発生することができます。

-   選択的な中断します。

    Windows XP 以降のオペレーティング システムで使用可能な唯一の代替手段では、USB セレクティブ サスペンドをサポートします。 この機能は、中断、デバイスがアイドル状態になった場合でも、システム自体は完全に operational 電源の状態 (S0) を維持制御する USB デバイス ドライバーを使用できます。 セレクティブ サスペンドは、USB 機能ドライバーをすべてサポートしている場合に特に強力です。 1 つでもドライバーではサポートされていない場合、CPU は C3 に入力できません。 セレクティブ サスペンドの詳細については、WDK を参照してください。

## <a name="which-usb-class-drivers-support-selective-suspend"></a>どの USB クラス ドライバーがセレクティブ サスペンドをサポートしますか。


セレクティブ サスペンドをサポートする Windows 8 の USB クラス ドライバーの一覧を次には。

-   Bluetooth

    このドライバーは、Windows XP Service Pack 2 および以降のバージョンの Windows を実行しているコンピューターで、デバイスをセレクティブ サスペンドことができます。 ドライバーでは、Bluetooth 無線構成記述子で自己給電とリモート ウェイクのビットを設定する必要があります。 ドライバー選択的に中断します (D2)、Bluetooth 無線 Bluetooth のアクティブな接続が存在しない場合。

-   USB HID

    このドライバーは HID デバイスをセレクティブ サスペンドことができます。 すべてのデバイス状態の変更にリモート ウェイク信号をトリガーするユーザーの責任になります。 HID スタックでセレクティブ サスペンドを有効にするには、デバイスの特定の VID+PID に、SelectiveSuspendEnabled レジストリ値を有効にする必要があります。 例については、Input.inf を参照してください。

    Windows 8 のコネクテッド スタンバイをサポートするシステムで、このドライバーは選択的なシステムがコネクテッド スタンバイ時 (D2) を中断します。 このドライバーでは、システムをスリープ解除でき、画面を有効にすることができます。

-   USB ハブ

    このドライバーはセレクティブ サスペンド ルートまたは外部ハブとデバイスが添付されていないことに、またはそのハブに接続されているすべてのデバイスを選択的に中断されることができます。

-   USB モデム

    アクティブなモデム接続が存在しない場合に、このドライバーは、デバイスをセレクティブ サスペンドことができます。

-   USB ストレージ (BOT)

    このドライバーは、これらのシステムがコネクテッド スタンバイに移動するときに Windows 8 のコネクテッド スタンバイをサポートするシステムで (D3) ストレージ デバイスをセレクティブ サスペンドことができます。 HID などがあるすべての Windows 8 システムで選択的に有効にするレジストリの上書きを中断します。

-   USB ストレージ (UAS)

    このドライバーはセレクティブ サスペンド (D3) 記憶装置がディスクのタイムアウト期間アイドル状態のとき。

-   USB ビデオ

    このドライバーは、Windows Vista およびそれ以降のオペレーティング システムで web カメラ (D3) をセレクティブ サスペンドことができます。

-   USB オーディオ

    このドライバーはセレクティブ サスペンド (D3) Windows 7 以降のオペレーティング システムでは、USB オーディオ デバイス、コンピューターがバッテリ電源上。

-   複合 USB

    このドライバーは、すべての子が中断の場合、(D3) 複合デバイスをセレクティブ サスペンドことができます。 D3 コールドをサポートするシステムで、すべての子は、D3 コールドを選択する必要があります。

-   USB スマート カード

    このドライバーは、既定では、Windows 7 およびそれ以降のオペレーティング システム (D2) スマート カード インターフェイス デバイスをセレクティブ サスペンドことができます。

-   汎用 USB 周辺機器 (WinUSB)

    このドライバーは、Windows Vista 以降のオペレーティング システムで既定で (D3) デバイスをセレクティブ サスペンドことができます。

-   WWAN:3 G または WiMax ドングル

    このドライバーは、デバイスをセレクティブ サスペンドことができます。 デバイス d2 に切り替わりが入力したアクティブなサブスクリプションがある場合に、アクティブなサブスクリプションがなくても、デバイスが D3 を入力します。

## <a name="why-cant-a-usb-device-awaken-windows-from-s3"></a>なぜことはできません、USB デバイスがスリープ解除 Windows S3 からでしょうか。


USB デバイスは、いくつかの理由から、次のように、S3 から Windows を呼び起こすことはできません。

1.  不適切な BIOS。

    最新の BIOS がコンピューターにインストールされていることを確認します。 コンピューターの最新の BIOS リビジョンを取得するには、OEM または ODM の Web サイトを参照してください。

2.  スリープ解除を有効になっていない BIOS。

    一部の Bios を使用すれば、S3 と S4 からのスリープ解除を無効にできます。 BIOS を S3 からスリープ解除が有効であることを確認します。

3.  USBBIOSx レジストリ キーが設定されていません。

    Windows XP のクリーン インストールでは、USBBIOSx レジストリ キーがありません。 OEM または ODM、BIOS を S3 からウェイクできることを検証して、このレジストリ キーを 0x00 に設定し、コンピューターを再起動します。

4.  ホスト コント ローラーには、S3 または S4 に電力はありません。

    多くの場合は、PC が低電力状態のときアドイン カードに電力を切り取ります。 アドイン カードに電源が入っていない場合、ウェイク イベントを検出することはできませんし、PC をスリープ解除することはできません。

詳細については、ヘルプとサポート センター Windows XP 以降のバージョンの Windows で USB のトラブルシューティングを参照してください。

## <a name="do-i-need-to-install-drivers-for-my-enhanced-usb-20-host-controller"></a>拡張 (USB 2.0) ホスト コント ローラー用ドライバーをインストールする必要がありますか。


次のバージョンの Windows では、USB 2.0 エンハンス ホスト コント ローラーをサポートします。

-   Windows Vista 以降
-   Windows Server 2003 以降
-   Windows XP Service Pack 1
-   Windows 2000 Service Pack 4

**注**  前に、USB 2.0 ハードウェアが使用可能なため、Windows 2000 および Windows XP がリリースされた、service pack は、これらのオペレーティング システムのドライバーがリリースされました。 ドライバーをインストールします。

1.  コンピューターに USB 2.0 ポートがあることと、エンハンス ホスト コント ローラー用ドライバーをインストールする必要があることを確認する最初の質問に対する回答で説明した手順に従います。
2.  デバイス マネージャー ウィンドウで、展開、**その他のデバイス**セクションの最初の質問で説明したようにし、ダブルクリック**ユニバーサル シリアル バス (USB) コント ローラー**します。
3.  **全般** タブのプロパティ ダイアログ ボックスで、次のようにクリックします。**ドライバーの再インストール**します。

    ![ドライバを再インストールします。](images/usb-reinstall-driver.jpg)

4.  新しいハードウェアの追加ウィザードで選択**ソフトウェアを自動的にインストール (推奨)**、順にクリックします**次**します。 ウィザードの最後のページをクリックするまで、すべての既定のオプションを使用して、ウィザードを続行**完了**します。 インストールを完了する、コンピューターを再起動する必要があります。

 

Windows XP Service Pack 1 での USB 2.0 の可用性に関する詳細については、マイクロソフト サポート技術情報の記事 329632 を参照してください"方法を取得し、USB 2.0 をインストールするドライバーを Windows XP Service pack 1"で[ http://support.microsoft.com/default.aspx?scid=KB;。EN-US;Q329632 &](https://support.microsoft.com/kb/329632)します。

**注**  コンピューターにインストールされている最新の更新プログラムがあることを確認するには、Windows 更新プログラムを定期的にアクセスします。

 

## <a name="can-i-disable-the-hi-speed-usb-device-plugged-into-non-hi-speed-usb-port-notice"></a>「高速 USB デバイスは非 HI-SPEED USB ポートに接続されている」通知を無効にできますか。


Windows XP および Windows の以降のバージョンは、高速をサポートしていない USB ポートに高速 USB デバイスが接続されているときにポップアップ通知が表示を作成します。 最速のパフォーマンスをデバイスから取得するには、ユーザーは、通知をクリックして、画面の指示に従って必要があります。

通知を無効にするには、次の手順に従います。

1.  この FAQ では、最初の質問」の説明に従って、デバイス マネージャーを起動します。
2.  デバイス マネージャー ウィンドウで、展開、**ユニバーサル シリアル バス コント ローラー**ノード。 タイトルに"Universal"または「開いている」という語があるホスト コント ローラーを探します。 いずれかの場合をダブルクリックします。
3.  **詳細**のタブ、**プロパティ**ダイアログ ボックスで、 **USB エラーを表示しない**します。

**注**  前の手順は、すべての USB 通知を無効にします、「高速 USB デバイスは高速ではないポートに接続されている」だけでなく。

 

Windows XP Service Pack 1 での USB 2.0 のサポートについては、マイクロソフト サポート技術情報の記事 329632 を参照してください"方法を取得し、USB 2.0 をインストールする Windows XP Service pack 1、ドライバーで[ http://support.microsoft.com/default.aspx?scid=KB;。EN-US;Q329632](https://support.microsoft.com/kb/329632)します。

## <a name="is-my-usb-20-hub-single-tt-or-multi-tt"></a>自分の USB 2.0 ハブ シングル TT またはマルチ TT ですか。


USB 2.0 ハブには、ハブ (単一 TT) 上のすべてのダウン ストリームに接続するポートの 1 つのトランザクション translator (TT) または (複数 TT) ハブのダウン ストリームに接続するポートごとに 1 つの TT ことができます。

値、 **bDeviceProtocol**の USB デバイスの記述子フィールドと**bInterfaceProtocol** USB インターフェイス記述子のフィールドを示すかどうか、ハブは、単一 TT またはマルチ TT:

-   シングル TT します。 **bDeviceProtocol** == 0x01
-   マルチ TT します。 **bDeviceProtocol** == 0x02

**Usbhub.sys**マルチ TT モードまたはシングル TT モードを有効にするこの設定を使用します。 Windows xp 以降、Usbhub.sys 常にモードを有効にマルチ TT マルチ TT ハブ。 TT レイアウトの詳細については、11.14.1.3 と 11.23.1 のセクションを参照してください、 [USB 2.0 仕様](http://www.usb.org/developers/docs)します。

## <a name="what-characters-or-bytes-are-valid-in-a-usb-serial-number"></a>どのような文字またはバイトは、USB シリアル番号で有効ですか。


USB デバイス記述子の**iSerialNumber**フィールド、デバイスのシリアル番号がかどうかと数が格納、次の手順を示します。

-   **iSerialNumber** 0x00 = =。USB デバイスのシリアル番号がありません。
-   **iSerialNumber** != 0x00 :USB デバイスには、シリアル番号があります。 割り当てられた値**iSerialNumber**シリアル番号の文字列のインデックスします。

デバイスのシリアル番号の場合、シリアル番号は、同じデバイスの各インスタンスを一意に識別する必要があります。

たとえば、2 つのデバイス記述子が、i の値で同じ**dVendor**、 **idProduct**と**bcdDevice** 、フィールド、 **iSerialNumber**フィールドは、他の 1 つのデバイスを区別するために、さまざまなである必要があります。

プラグ アンド プレイでは、USB シリアル番号のすべてのバイト有効である必要があります。 1 バイトが有効でない場合、Windows は、シリアル番号を破棄し、シリアル番号がなかったかのように、デバイスを処理します。 次のバイト値は有効で USB シリアル番号のないです。

-   -   0x2C します。
-   0x20 より小さい値です。
-   0x7F よりも大きい値です。

詳細については、 **iSerialNumber**値の 9.6.1」セクションを参照してください、 [USB 2.0 仕様](http://www.usb.org/developers/docs)します。

## <a name="what-langid-is-used-in-a-string-request-on-localized-builds-of-windows"></a>どのような LANGID が Windows のローカライズされたビルド文字列の要求で使用されるでしょうか。


USB デバイスでは、シリアル番号の文字列のインデックスに USB デバイス記述子の iSerialNumber フィールドを設定してシリアル番号の有無を示します。 シリアル番号を取得するには、Windows では、0x0409 (米国に設定する言語識別子 (LANGID) を持つ文字列要求を発行します。英語のみ)。 Windows では、他の言語にローカライズされた Windows のバージョンの場合でも、USB シリアル番号を取得するのにこの LANGID 常に使用します。

## <a name="what-langid-is-used-to-extract-a-devices-serial-number"></a>どのような LANGID はデバイスのシリアル番号を抽出するために使用しますか?


USB デバイスでは、シリアル番号の文字列のインデックスに USB デバイス記述子の iSerialNumber フィールドを設定してシリアル番号の有無を示します。 シリアル番号を取得するには、Windows では、0x0409 (米国に設定する言語識別子 (LANGID) を持つ文字列要求を発行します。英語のみ)。 Windows では、他の言語にローカライズされた Windows のバージョンの場合でも、USB シリアル番号を取得するのにこの LANGID 常に使用します。

## <a name="what-is-the-maximum-usb-transfer-size-for-different-windows-versions"></a>さまざまな Windows バージョンの最大の USB 転送サイズとは何ですか。


参照してください[さまざまなオペレーティング システム上の USB の最大サイズの転送](https://support.microsoft.com/kb/832430)します。

## <a name="how-should-numbers-be-assigned-to-multiple-interfaces-on-a-composite-device"></a>番号は、複合デバイスに複数のインターフェイスにどのように割り当てする必要がありますか。


Windows では、USB デバイスを最初の構成では、複数のインターフェイスを持つ複合デバイスとして扱われます。

Windows XP Service Pack 1 および Windows の以前のバージョン。

-   インターフェイス番号は 0 から始まるである必要があります。
-   インターフェイス番号は、連続して増加である必要があります。

Windows XP Service Pack 2 および以降のバージョンの Windows では、インターフェイスの番号は増加、連続しないにのみ必要です。

インターフェイス番号の詳細については、次を参照してください。[インタ フェースが順番に番号付けされていない複合 USB デバイスが Windows XP では動作しない](https://support.microsoft.com/kb/814560)します。

インターフェイスの代替設定は、すべてのバージョンの Windows には、次のように割り当てる必要があります。

-   インターフェイスの既定値は 0 を設定する代替では常にします。
-   その他の代替設定の数値は、連続して増加である必要があります。

代替の設定の詳細については、の 9.6.5」セクションを参照してください。、 [USB 2.0 仕様](http://www.usb.org/developers/docs)します。

## <a name="what-are-the-major-restrictions-imposed-by-usbccgpsys"></a>Usbccgp.sys によって課される主要な制約とは


**Usbccgp.sys**複合デバイスをサポートしています。

-   Windows Me
-   Windows XP
-   Windows Server 2003
-   Windows Vista
-   Windows Server 2008

読み込みが可能にある可能性がありますが**Usbhub.sys**として複合デバイス以降では、これらの親のドライバーのバージョンの Windows、Microsoft は推奨していませんので、ハードウェアの互換性エラーが発生する可能性があります。 使用する必要があります**で、Usbccgp.sys**代わりにします。

複合デバイスの適切なドライバーをロードすることを確認するには、よう INF ファイルでインクルードし、ニーズのディレクティブを使用します。

``` syntax
Include = USB.INF
Needs = Composite.Dev
```

ハードウェア デバイスとドライバーを主な制限が課せられる**で、Usbccgp.sys**次に示します。

-   Usbccgp のみ既定構成 0 の構成をサポートします。
-   Usbccgp サポートしていませんセレクティブ サスペンド Windows XP および Windows Server 2003 で。 この機能は、Windows Vista および Windows の以降のバージョンでのみサポートされます。
    **注**   Usbccgp でセレクティブ サスペンドをサポート Windows XP SP1、Windows XP では、機能制限付きで以降のバージョンでします。 これらのバージョンの Windows デバイスの場合は、各子関数に保留中のアイドル状態の IRP がある場合にのみ、複合デバイスがセレクティブ サスペンドに配置します。 Usbccgp ではサポートされないセレクティブ サスペンド Windows XP RTM

     

-   Usbccgp では、Windows XP SP2、Windows Server 2003 SP1 では、以降のバージョンの Windows でのみ、インターフェイスの関連付け記述子 (IAD) をサポートしています。
-   Usbccgp は、Windows XP SP2、Windows Server 2003 SP1 では、以降のバージョンの Windows でのみ、連続しない複数のインターフェイスの番号をサポートします。

## <a name="how-do-i-enable-debug-tracing-for-usb-core-binaries"></a>USB の主要なバイナリのデバッグ トレースを有効にする方法


に関するブログの投稿を参照してください。[を含めると、ドライバーのパブリックの PDB ファイルに WPP トレース メッセージを表示する方法](http://blogs.msdn.com/b/usbcoreblog/archive/2013/06/29/wpp-blog-post.aspx)します。

USB core スタックのデバッグに関する詳細については、次を参照してください。[ドライバーとサブシステムのさまざまな詳細なデバッグ トレースを有効にする方法](https://support.microsoft.com/kb/314743)します。

## <a name="does-windows-support-interface-association-descriptors"></a>Windows は、インターフェイスの関連付けの記述子をサポートしますか。


[はい]。 USB 2.0 インターフェイスの関連付け記述子 (IAD) エンジニア リングの変更通知 (ECN) には、インターフェイスのグループ化し、関数内での代替設定を記述するための新しい標準的な方法が導入されました。 IAD は、2 つ以上連続するインターフェイスと 1 つの関数内での代替設定を識別するために使用できます。

Microsoft は現在、IAD をサポートするデバイスを開発する Ihv で作業します。 次のオペレーティング システムでは、IAD サポートがあります。

-   Windows XP Service Pack 2 以降
-   Windows Server 2003 Service Pack 1 以降
-   Windows Vista

## <a name="does-the-usb-stack-handle-chained-mdls-in-a-urb"></a>USB スタックのハンドルは、URB で MDLs チェーンされているか。


この機能は Windows に含まれている USB 3.0 ドライバー スタックがサポートされます。

## <a name="can-a-driver-have-more-than-one-urb-in-an-irp"></a>ドライバーは IRP の 1 つ以上の URB を持つことができますか。


No. この機能は Windows に含まれている USB スタックによってサポートされていません。

## <a name="does-windows-support-usb-composite-hubs"></a>Windows は、複合の USB ハブをサポートしますか。


多機能の USB デバイス - とも呼ばれます - 複合 USB デバイスは、それぞれが独立したデバイスとして処理できる、複数の関数を公開します。 USB の一般的な親ドライバーが読み込まれます**で、Usbccgp.sys**デバイスの機能の eaech の親ドライバーとして機能します。 一般的な親の USB ドライバーが別の USB デバイスと PDO を作成し、関数ごとにデバイス スタックを構築しますかのように複合デバイスの機能を列挙します。

複合 USB デバイスがハブとして機能する関数を公開できません。 Windows にこのようなハブが正しく列挙できませんし、システム クラッシュが発生する可能性があります、デバイスをインストールしようとします。

## <a name="where-can-i-find-additional-faqs-on-usb"></a>USB の他の Faq はどこで入手できますか。


USB を参照してください-IF FAQ ページ<http://www.usb.org/developers/usbfaq/>します。

## <a name="related-topics"></a>関連トピック
[すべての開発者の USB の概念](usb-concepts-for-all-developers.md)  
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  




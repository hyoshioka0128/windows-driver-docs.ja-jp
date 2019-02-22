---
Description: This section introduces you to USB driver development.
title: USB クライアント ドライバー開発を入門
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f55df5b190d698be6ddd7e53d533e45af3bbbdc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560752"
---
# <a name="getting-started-with-usb-client-driver-development"></a>USB クライアント ドライバー開発を入門


このセクションでは、USB ドライバーの開発を紹介します。 ドライバーの開発に慣れていない場合に、セクションが適用されます。Microsoft が、インボックス ドライバーを行いません、USB デバイスのドライバーを実装します。 このようなドライバーと呼ばれる、 *USB クライアント ドライバー*このドキュメントで設定します。 このセクションのトピックでは、USB の高度な概念について説明し、USB クライアント ドライバーの一般的なタスクを実行する詳細な手順を提供します。 これらの概念の詳細についてでの USB 仕様を参照してください。 [USB ドキュメント](https://go.microsoft.com/fwlink/p/?linkid=617552)します。

ドライバー開発者は、コーディング、C プログラミング言語での経験があるし、関数ポインター、コールバック関数、およびイベント ハンドラーの概念を理解する必要があります。 ユーザー モード ドライバー フレームワークに基づくドライバーを書き込み、ことを確認する場合は、理解するおくと、C++ と COM

## <a name="learning-path-for-usb-client-driver-developers"></a>USB クライアント ドライバー開発者向けのラーニング パス


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>学習手順</th>
<th>手順を完了するにできる必要があります.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>手順 1.</strong>、読み取り、<a href="https://go.microsoft.com/fwlink/p/?linkid=617552" data-raw-source="[Official USB specification version 2.0 and 3.0](https://go.microsoft.com/fwlink/p/?linkid=617552)">公式 USB 仕様のバージョン 2.0 および 3.0</a>します。</p></td>
<td>業界の仕様とアーキテクチャのさまざまなコンポーネント (デバイス、ホスト コント ローラーとハブ) について説明します。 これは、&#39;データ フロー モデルを理解することが重要に相互通信と、デバイスが要求される要求の形式とのホストとデバイスの通信する方法。</td>
</tr>
<tr class="even">
<td><p><strong>手順 2</strong>: テストの USB デバイスを取得します。</p></td>
<td><ul>
<li>USB デバイスとそのハードウェアの仕様があります。 仕様では、デバイスの機能とサポートされているベンダー コマンドについて説明します。 仕様を使用すると、デバイス ドライバーとの関連の設計に関する決定の機能を確認できます。</li>
<li>OSR USB FX2 ラーニング キットは、USB ドライバーの開発に慣れていない場合があります。 キットは、このドキュメント セットに含まれる USB サンプルを調べる最も適しています。 ラーニング キットを入手することができます<a href="https://go.microsoft.com/fwlink/p/?linkid=617553" data-raw-source="[OSR Online](https://go.microsoft.com/fwlink/p/?linkid=617553)">OSR オンライン</a>します。</li>
<li>Microsoft USB Test Tool (MUTT) デバイスを持っています。 MUTT ハードウェアを購入できる<a href="https://go.microsoft.com/fwlink/p/?linkid=617554" data-raw-source="[JJG Technologies](https://go.microsoft.com/fwlink/p/?linkid=617554)">JJG テクノロジ</a>します。 デバイスのファームウェアがインストールされているインストールではありません。 ファームウェアをインストールする<a href="https://go.microsoft.com/fwlink/p/?linkid=617555" data-raw-source="[download the MUTT software package](https://go.microsoft.com/fwlink/p/?linkid=617555)">MUTT ソフトウェア パッケージをダウンロード</a>MUTTUtil.exe を実行します。 詳細については、パッケージに付属のマニュアルを参照してください。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>手順 3</strong>、調査、 <a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB デバイスのレイアウト</a>と、関連<a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">の USB ディスクリプター</a>します。</p></td>
<td>構成記述子、インターフェイスの記述子のサポートされている各代替設定、およびそのエンドポイント記述子を読み取ることによって、デバイスの機能について説明します。 使用して<a href="https://go.microsoft.com/fwlink/p/?linkid=617556" data-raw-source="[USBView](https://go.microsoft.com/fwlink/p/?linkid=617556)">USBView</a>すべて USB コント ローラーを参照することができます、および USB デバイスが、それらに接続されているし、デバイスの構成を調べることもできます。</td>
</tr>
<tr class="even">
<td><p><strong>手順 4</strong>—<a href="winusb-considerations.md" data-raw-source="[Choose a driver model for developing a USB client driver](winusb-considerations.md)">USB クライアント ドライバーを開発するためのドライバー モデルを選択する</a>します。</p></td>
<td>カスタム ドライバーを作成またはデバイスのデザインに基づく Microsoft から提供されたドライバーのいずれかを使用する必要があるかどうかを決定します。 ドライバーを記述するため、最適なドライバー モデルを選択し、各モデルでサポートされている機能について説明します。</td>
</tr>
<tr class="odd">
<td><p><strong>手順 5</strong>— Microsoft 提供の USB ドライバー スタックとドライバー開発の概念を理解します。</p>
<ul>
<li><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows での USB ホスト側のドライバー</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff554731" data-raw-source="[Concepts for All Driver Developers](https://msdn.microsoft.com/library/windows/hardware/ff554731)">すべてのドライバー開発者向けの概念</a></li>
<li><a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">すべての USB 開発者の概念</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff554721" data-raw-source="[Device nodes and device stacks](https://msdn.microsoft.com/library/windows/hardware/ff554721)">デバイス ノードとデバイス スタック</a></li>
<li><em>Windows Driver Foundation でのドライバーの開発</em>少額 Orwick と Guy Smith によって書き込まれた、します。 詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/dn605830" data-raw-source="[Developing Drivers with WDF](https://msdn.microsoft.com/library/windows/hardware/dn605830)">WDF のドライバーが開発</a>します。</li>
<li><a href="usb-driver-samples-in-wdk.md" data-raw-source="[USB driver samples](usb-driver-samples-in-wdk.md)">USB ドライバーのサンプル</a></li>
</ul></td>
<td><ul>
<li>Windows オペレーティング システムでのドライバーのしくみの基礎を理解します。 基本事項を把握すると、適切な設計上の決定を行い、開発プロセスを効率化することは役立ちます。</li>
<li>ユーザー モードとカーネル モードのドライバーのアーキテクチャ モデルを区別します。</li>
<li>ドライバーの読み込みと Windows がデバイス ツリーとデバイス ノードのプラグ アンド プレイ (PnP) デバイスを整理する方法を理解します。 PnP マネージャーのビルド デバイス スタックと、デバイス スタックでは、ドライバーとそのデバイス オブジェクトを配置する場所についても理解する必要があります。</li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>手順 6</strong>など、開発とデバッグ環境を準備します。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617580" data-raw-source="[Install the latest Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=617580)">最新の Windows Driver Kit (WDK) のインストール</a>します。</li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617580" data-raw-source="[Install Microsoft Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=617580)">Microsoft Visual Studio 2012 をインストール</a>します。</li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh450944" data-raw-source="[Get Set Up for Debugging](https://msdn.microsoft.com/library/windows/hardware/hh450944)">デバッグの設定を取得</a>します。</li>
<li>あることを確認、<a href="headers-and-libraries-for-a-usb-client-driver.md" data-raw-source="[Headers and libraries required by a USB client driver](headers-and-libraries-for-a-usb-client-driver.md)">ヘッダーとライブラリの USB クライアント ドライバーで必要な</a>します。</li>
</ul></td>
<td><ul>
<li>カーネル モード ドライバーを記述する必要がありますを構成した場合、イーサネット ネットワークを 1394 ケーブル、USB 2.0 または 3.0 デバッグ ケーブル、またはヌル モデム ケーブルを介したホストとターゲット コンピューターでデバッグします。</li>
<li>ユーザー モード ドライバーを記述する場合は、Microsoft Visual Studio 環境で使用可能なユーザー モード デバッガーを使用できます。 知っておくべき<a href="https://msdn.microsoft.com/library/windows/hardware/hh406273" data-raw-source="[how to attach to a process or launch a process under the debugger](https://msdn.microsoft.com/library/windows/hardware/hh406273)">プロセスにアタッチするか、デバッガーでプロセスを起動する方法</a>します。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>手順 7</strong>:、最初のドライバーを作成します。</p>
<ul>
<li><a href="tutorial--write-your-first-usb-client-driver--kmdf-.md" data-raw-source="[How to write your first USB client driver (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)">最初、USB クライアント ドライバー (KMDF) を記述する方法</a></li>
<li><a href="implement-driver-entry-for-a-usb-driver--umdf-.md" data-raw-source="[How to write your first USB client driver (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)">最初、USB クライアント ドライバー (UMDF) を記述する方法</a></li>
</ul></td>
<td>作成、ビルド、および Visual Studio 2012 に含まれている USB テンプレートを使用して、最初の USB クライアント ドライバーをインストールします。 フレームワーク ドライバー、デバイス、およびキューのオブジェクトを記述し、フレームワーク、ドライバーとの通信方法を理解することができます。</td>
</tr>
<tr class="even">
<td><strong>手順 8</strong>-USB 制御転送要求を送信することによって、ドライバーを拡張します。</td>
<td>標準のコントロール要求、仕入先のコマンドをデバイスに送信します。 詳細については、次を参照してください。 <a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">USB 制御転送を送信する方法</a>します。</td>
</tr>
<tr class="odd">
<td><p><strong>手順 9</strong>-拡張、ドライバーを WDF USB I/O ターゲットのオブジェクトを使用して USB データ転送を実行します。 <a href="usb-device-i-o.md" data-raw-source="[USB data transfers](usb-device-i-o.md)">データ転送の USB</a>します。</p></td>
<td><p>一般的なタスクを実行するには、ドライバーを拡張します。 このトピックで、&quot;方法&quot;それらのタスクに関するステップ バイ ステップ ガイダンスを提供する、このドキュメント セットのトピックです。</p>
<ul>
<li><a href="wdk-resources-for-usb-driver-development.md" data-raw-source="[Common tasks for USB client drivers](wdk-resources-for-usb-driver-development.md)">USB クライアント ドライバーに関する一般的なタスク</a></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="community-resources-for-usb"></a>USB のコミュニティ リソース


<a href="" id="microsoft-windows-usb-core-team-blog"></a>[Microsoft Windows USB コア チームのブログ](https://go.microsoft.com/fwlink/p/?linkid=617581)  
Microsoft USB チームが作成した投稿をご覧ください。 ブログは、さまざまな USB ホスト コント ローラーと Windows PC の USB ハブで動作する Windows USB ドライバー スタックについて説明します。 USB クライアント ドライバー開発者および USB ハードウェアの設計者の役に立つリソースでドライバー スタック実装の理解し、一般的な問題を解決するトレースを収集するためのツールを使用する方法について説明し、ログ ファイル。

<a href="" id="osr-online-lists---ntdev"></a>[OSR オンライン リスト -:ntdev](https://go.microsoft.com/fwlink/p/?linkid=617582)  
によって管理されるディスカッション リスト[OSR オンライン](https://go.microsoft.com/fwlink/p/?linkid=617590)カーネル モード ドライバー開発者向け。

<a href="" id="usb-technologies"></a>[USB テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=617583)  
その他のリソースに頻繁に基づく寄せられる質問の開発者から USB デバイスと Windows オペレーティング システムで動作するドライバーを開発するは初めてです。

<a href="" id="windows-dev-center-for-hardware-development"></a>[Windows ハードウェア開発のデベロッパー センター](https://go.microsoft.com/fwlink/p/?linkid=617584)  
[ドライバーの開発用最新ツールをダウンロード](https://go.microsoft.com/fwlink/p/?linkid=617585)、お使いの製品が信頼性が高く、を通じて Windows と互換性があることを確認、 [Windows 認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=617591)、学習[Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507).

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB) ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[USB のセレクティブがサスペンドを有効にする方法と、USB デバイスの UMDF ドライバーにシステムがスリープ解除](https://go.microsoft.com/fwlink/p/?linkid=617587)  
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  




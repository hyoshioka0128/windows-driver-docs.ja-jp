---
Description: USB デバイスとドライバーをテストに使用できるさまざまなツールについて説明します。
title: USB テスト ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b3155c1af400918332470821c43df3d9b82358
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377201"
---
# <a name="usb-test-tools"></a>USB テスト ツール


USB デバイスとドライバーをテストに使用できるさまざまなツールについて説明します。

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
<td><p><a href="muttutil.md" data-raw-source="[MuttUtil](muttutil.md)">MuttUtil</a></p></td>
<td><p>MuttUtil に対してさまざまなタスクを実行します<a href="microsoft-usb-test-tool--mutt--devices.md" data-raw-source="[MUTT devices](microsoft-usb-test-tool--mutt--devices.md)">MUTT デバイス</a>します。</p>
<ul>
<li>テスト デバイスのファームウェアを更新します。</li>
<li>MUTT デバイス用のドライバーをインストールします。</li>
<li>デバイスがエラーなしにインストールされていることを確認します。</li>
<li>デバイスの動作のバス速度を変更します。</li>
<li>指定した期間後に再開ウェイク信号を送信するデバイスを構成します。</li>
<li>MUTT パックでは、完全なまたは高速度で動作するハブを設定します。としてシングル TT またはマルチ TT ハブです。</li>
</ul>
<p>テスト デバイスが最新のファームウェアに正しくアップグレードされたことを確認するには含まれているテスト スクリプトのインストール」セクションでは、MuttUtil 埋め込まれます。 ツールが含まれ、 <a href="https://go.microsoft.com/fwlink/p/?linkid=617710" data-raw-source="[MUTT Software Package](https://go.microsoft.com/fwlink/p/?linkid=617710)">MUTT ソフトウェア パッケージ</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-device-to-select-suspend.md" data-raw-source="[USB client driver verifier](how-to-send-a-usb-device-to-select-suspend.md)">USB クライアント ドライバーの検証ツール</a></p></td>
<td><p>このトピックでは、により、特定のエラー ケースをテストするクライアント ドライバーを USB 3.0 ドライバー スタックの USB クライアント ドライバーの検証の機能について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-retrieve-information-about-a-usb-device.md" data-raw-source="[USB hardware verifier (USB3HWVerifierAnalyzer.exe)](how-to-retrieve-information-about-a-usb-device.md)">USB ハードウェア検証ツール (USB3HWVerifierAnalyzer.exe)</a></p></td>
<td><p>このトピックでは、テストと特定のハードウェアのイベントのデバッグに使用する USB ハードウェア検証ツール (USB3HWVerifierAnalyzer.exe) について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usblpm-tool.md" data-raw-source="[USBLPM](usblpm-tool.md)">USBLPM</a></p></td>
<td><p>USBLPM ツールでは、USB 3.0 ポートの U0 U1 と U2/U3 電源の状態を監視します。 U0/U1 と U2 間の遷移が正しく発生することを確認することにも使用できます。 さらに、ツールは、有効またはシステムのすべてのデバイスで U1 および U2 の状態を無効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usbstress.md" data-raw-source="[USBStress](usbstress.md)">USBStress</a></p></td>
<td><p>USBStress がユーザー モード アプリケーション (usbstress.exe) と、カーネル モード ドライバーのドライバーのインストール パッケージの組み合わせ usbstress.sys します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usbtcd.md" data-raw-source="[USBTCD](usbtcd.md)">USBTCD</a></p></td>
<td><p>USBTCD は、ユーザー モード アプリケーションとカーネル モード ドライバーの組み合わせです。 ツールを実行します。 読み取りおよび書き込み操作です。 さまざまな転送の長さにし、テスト デバイスからの一括、アイソクロナス、データ転送、コントロールを開始します。 SuperMUTT デバイスの場合は、USBTCD は、一括エンドポイントでサポートされているストリームにデータを転送します。 転送バッファー連鎖 MDLs としても送信できます。 その場合は、転送バッファー内のセグメントの数を指定できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-xhciwmi.md" data-raw-source="[USB XHCIWMI](usb-xhciwmi.md)">USB XHCIWMI</a></p></td>
<td><p>XHCIWMI は、診断用のツールです。 のみ、このツールは、Windows 8 上で実行し、デバイスが xHCI ポートに接続して Windows には、Microsoft USB 3.0 ドライバー スタックが読み込まれる情報を収集します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB の診断結果とテスト ガイド](usb-driver-testing-guide.md)  




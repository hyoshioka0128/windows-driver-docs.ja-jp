---
Description: MUTT ソフトウェアパッケージには、MUTT デバイスで使用するためのツールがいくつか含まれています。 一連のツールには、ファームウェアアップグレードアプリケーション、ドライバーインストールパッケージ、デバイスに転送を送信するアプリケーションが含まれます。
title: MUTT ソフトウェア パッケージに含まれるツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb006513d071d7f7ca8a5cb8919df593ed9e0b76
ms.sourcegitcommit: b7ba0d42117f30125ae2dcd4dcb16dd988a18ff3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72303926"
---
# <a name="tools-in-the-mutt-software-package"></a>MUTT ソフトウェア パッケージに含まれるツール


**最終更新日時:**

-   2019年2月

**適用対象:**

-   Windows 10
-   Windows 8.1
-   Windows 8

MUTT ソフトウェアパッケージには、 [mutt デバイス](microsoft-usb-test-tool--mutt--devices.md)で使用するためのツールがいくつか含まれています。 一連のツールには、ファームウェアアップグレードアプリケーション、ドライバーインストールパッケージ、デバイスに転送を送信するアプリケーションが含まれます。

## <a name="download-mutt-software-package"></a>MUTT ソフトウェアパッケージのダウンロード


Microsoft USB Test Tool (MUTT) ソフトウェアパッケージには、Microsoft usb ドライバースタックと USB コントローラーまたはハブの相互運用性をテストするための、ハードウェアテストエンジニア向けのテストツールが含まれています。 付属のドキュメントでは、さまざまな種類の MUTT ハードウェアの概要を簡単に説明し、コントローラー、ハブ、デバイス、BIOS/UEFI テストのトポロジを提案します。 また、このドキュメントには、テストの実行方法、USB ドライバースタックでのイベントのトレース方法、カーネルデバッガーでの情報のキャプチャ方法に関する情報も含まれています。

ファイル名: mutt2_94

9.3 MB

[![download ソフトウェアパッケージのダウンロード](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)

## <a name="version-updates"></a>バージョンの更新

バージョン2.9.4 の変更

- USB タイプの更新-C SuperMUTT ファームウェア (v54)
- USB4 スイッチで動作するように USB 接続 Exerciser ソフトウェアを更新する

バージョン2.9.3 の変更

- ドライバー署名の問題の修正
- ARM64 テストツールを含める

バージョン2.9 の変更点

- USB タイプの更新-C SuperMUTT ファームウェア (v53)

バージョン2.8 の変更点

- HLK UCSI テストとの互換性を向上させるために、USB タイプ C を更新しました。

バージョン2.7 の変更点

- USB タイプ C のファームウェア、ツール、およびドキュメントを更新しました。 HLK UCSI テストと互換性があります。

バージョン2.4 の変更点

-   USB タイプ C SuperMUTT ファームウェア、ツール、およびドキュメントの初期ドロップを含みます。

バージョン2.2 の変更点

-   USB 接続 Exerciser ツールを含む

バージョン2.0 の変更点

-   SuperMUTT ファームウェアがバージョン45に更新されました。
-   WinUSB 転送テストが更新されました。

バージョン1.9.1 の変更

-   バージョン1.9 以前では、システムによっては、システムが S4 から再開された後に、xHCI コントローラーに接続されているときに、大規模なデバイスが非常に高速に列挙されます。 バージョン1.9.1 はその問題を修正します。

バージョン1.9 の変更点

-   SuperMUTT は、デバイスの MS OS 記述子を読み取って、既定で WinUSB ドライバーを読み込みます。
-   WinUSB でのスーパー Mutt は、既定ではセレクティブサスペンドをサポートしています。

## <a name="tools-in-the-package"></a>パッケージ内のツール


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>テストツール</th>
<th>説明</th>
<th>Filename</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="usbtcd.md" data-raw-source="[USBTCD](usbtcd.md)">USBTCD</a></td>
<td><ul>
<li>USBTCD は、カーネルモードドライバー (USBTCD) と通信し、さまざまな長さの転送サイズを持つ一般的な USB データ転送シナリオを実行するアプリケーション (USBTCD) です。</li>
<li>ドライバーのインストールファイルは、USBTCD および USBTCD です。</li>
<li>FX3Perf は、スーパー Mutt デバイスが接続されている USB コントローラーの読み取りパフォーマンスを測定します。</li>
</ul></td>
<td><p>USBTCD</p>
<p>USBTCD</p>
<p>USBTCD</p>
<p>FX3Perf</p>
<p>UsbTCDTransferTest .bat</p></td>
</tr>
<tr class="even">
<td></td>
<td><ul>
<li>システム上の USB 3.0 ホストコントローラおよび USB 3.0 ハブに関する情報を収集して、問題のあるファームウェアのリビジョンを特定し、更新を提案します。</li>
<li>既知の問題をフィルター処理するには、このテストを他のテストの前に実行することをお勧めします。 Windows 8 でのみ実行されます。</li>
</ul></td>
<td>xhciwmi</td>
</tr>
<tr class="odd">
<td><a href="usb-xhciwmi.md" data-raw-source="[XHCIWMI](usb-xhciwmi.md)">XHCIWMI</a><a href="usblpm-tool.md" data-raw-source="[USBLPM](usblpm-tool.md)">USBLPM</a></td>
<td><ul>
<li>USB 3.0 ポートの U0/U1/U2/U3 の電源状態を監視します。</li>
<li>U0/U1/U2 間の移行が正しく行われていることを確認します。</li>
</ul></td>
<td>UsbLPM .exe</td>
</tr>
<tr class="even">
<td><a href="usbstress.md" data-raw-source="[USBStress](usbstress.md)">USBStress</a></td>
<td><ul>
<li>USBStress アプリケーションは、カーネルモードドライバー (usbstress .sys) と通信し、一般的な USB データ転送シナリオを実行します。</li>
<li>ドライバーのインストールファイルは、usbstress. sys と usbstress です。</li>
<li>UsbStressTest ファイルは、ドライバーのインストール後にすべてのデータ転送テストを実行します。</li>
</ul></td>
<td><p>usbstress .exe</p>
<p>usbstress .inf</p>
<p>usbstress. sys</p>
<p>UsbStressTest</p></td>
</tr>
<tr class="odd">
<td><a href="muttutil.md" data-raw-source="[MuttUtil](muttutil.md)">MuttUtil</a></td>
<td><ul>
<li>テストデバイスのファームウェアを更新します。</li>
<li>MUTT デバイス用のドライバーをインストールします。</li>
<li>デバイスがエラーなしでインストールされていることを確認します。</li>
<li>デバイスのオペレーティングバス速度を変更します。</li>
<li>指定した期間が経過した後に、再開スリープ解除信号を送信するようにデバイスを構成します。</li>
<li>MUTT パックでは、完全または高速度で動作するようにハブを設定します。単一の TT またはマルチ TT ハブとして。</li>
</ul></td>
<td><p>MuttUtil</p></td>
</tr>
<tr class="even">
<td><a href="how-to-retrieve-information-about-a-usb-device.md" data-raw-source="[USB hardware verifier](how-to-retrieve-information-about-a-usb-device.md)">USB ハードウェア検証ツール</a></td>
<td>すべてのハードウェアイベントをコンソールに表示します。</td>
<td>USB3HWVerifierAnalyzer</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB テストツール (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  




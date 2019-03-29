---
Description: The MUTT software package contains several tools to be used with MUTT devices. The suite of tools include firmware upgrade application, driver installation package, and applications that send transfers to the device.
title: MUTT ソフトウェア パッケージに含まれるツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3f3455ee8f9f9db1e66b9b04dc009b602d38d8
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743439"
---
# <a name="tools-in-the-mutt-software-package"></a>MUTT ソフトウェア パッケージに含まれるツール


**最終更新日。**

-   2019 年 2 月

**適用対象します。**

-   Windows 10
-   Windows 8.1
-   Windows 8

MUTT ソフトウェア パッケージにはで使用するいくつかのツールが含まれています[MUTT デバイス](microsoft-usb-test-tool--mutt--devices.md)します。 ツールのスイートには、ファームウェア アップグレード アプリケーション、ドライバーのインストール パッケージ、およびデバイスに転送を送信するアプリケーションが含まれます。

## <a name="download-mutt-software-package"></a>MUTT ソフトウェア パッケージをダウンロードします。


Microsoft USB Test Tool (MUTT) ソフトウェア パッケージには、ハードウェア テスト エンジニアが、USB コント ローラーまたはハブは Microsoft USB ドライバー スタックとの相互運用性をテストするためのテスト ツールが含まれています。 付属のマニュアルでは、MUTT ハードウェアのさまざまな種類の概要を簡単に説明し、コント ローラー、ハブ、デバイス、および BIOS および UEFI テストのトポロジを提案します。 ドキュメントには、USB ドライバー スタックのトレース イベント、テストを実行して、カーネル デバッガー内の情報をキャプチャする方法の手順に関する情報も含まれています。

ファイル名: mutt2_9.msi

7.3 MB

[![mutt ソフトウェア パッケージをダウンロードします。](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)

## <a name="version-updates"></a>バージョンの更新

バージョン 2.9 の変更

- 更新された USB 型 C SuperMUTT ファームウェア (v53)

バージョン 2.8 の変更

- HLK UCSI テスト互換性の向上のため USB 型 C SuperMUTT ファームウェアを更新します。

バージョン 2.7 の変更

- 更新された USB 型 C SuperMUTT ファームウェア、ツール、およびドキュメント。 HLK UCSI との互換性をテストします。

バージョン 2.4 の変更

-   USB タイプ C SuperMUTT ファームウェア、ツール、およびドキュメントの最初のドロップが含まれています。

Version 2.2 の変更

-   USB 接続 Exerciser ツールが含まれています

バージョン 2.0 の変更

-   バージョン 45 に SuperMUTT ファームウェアを更新します。
-   更新された WinUSB 転送をテストします。

1.9.1 のバージョンの変更

-   1.9 と一部のシステムでは、以前のバージョンでは、システム後の列挙 (xHCI コント ローラーに接続されている) 場合、高速で SuperMutt デバイス S4 から再開されます。 バージョン 1.9.1 では、その問題を修正します。

バージョン 1.9 の変更

-   SuperMUTT は、デバイスの OS の MS 記述子を読み取ることで、既定で WinUSB ドライバーを読み込みます。
-   既定で選択的 WinUSB サポートに superMUTT を中断します。

## <a name="tools-in-the-package"></a>パッケージ内のツール


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>テスト ツール</th>
<th>説明</th>
<th>Filename</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="usbtcd.md" data-raw-source="[USBTCD](usbtcd.md)">USBTCD</a></td>
<td><ul>
<li>USBTCD は、カーネル モード ドライバー (USBTCD.sys) と通信し、さまざまな長さの転送サイズの一般的な USB データの転送シナリオを実行するアプリケーション (USBTCD.exe) です。</li>
<li>ドライバーのインストール ファイルは、USBTCD .sys と USBTCD.inf です。</li>
<li>FX3Perf.bat は、SuperMUTT デバイスが接続されている USB コント ローラーの読み取りのパフォーマンスを測定します。</li>
</ul></td>
<td><p>USBTCD.exe</p>
<p>USBTCD.sys</p>
<p>USBTCD.inf</p>
<p>FX3Perf.bat</p>
<p>UsbTCDTransferTest.bat</p></td>
</tr>
<tr class="even">
<td></td>
<td><ul>
<li>問題のあるファームウェアのリビジョンを識別し、更新プログラムを提案するシステムで、USB 3.0 ホスト コント ローラーと USB 3.0 ハブに関する情報を収集します。</li>
<li>その他の任意のテストを既知の問題をフィルター処理する前に、このテストを実行することをお勧めします。 Windows 8 でのみ実行されます。</li>
</ul></td>
<td>xhciwmi.exe</td>
</tr>
<tr class="odd">
<td><a href="usb-xhciwmi.md" data-raw-source="[XHCIWMI](usb-xhciwmi.md)">XHCIWMI</a><a href="usblpm-tool.md" data-raw-source="[USBLPM](usblpm-tool.md)">USBLPM</a></td>
<td><ul>
<li>USB 3.0 ポートの U0 U1 と U2/U3 電源の状態を監視します。</li>
<li>U0/U1 と U2 間の遷移が正しく発生することを確認します。</li>
</ul></td>
<td>UsbLPM.exe</td>
</tr>
<tr class="even">
<td><a href="usbstress.md" data-raw-source="[USBStress](usbstress.md)">USBStress</a></td>
<td><ul>
<li>アプリケーションは、カーネル モード ドライバー (usbstress.sys) と通信し、USB データの一般的な実行 USBStress シナリオを転送します。</li>
<li>ドライバーのインストール ファイルは、usbstress.sys と usbstress.inf です。</li>
<li>UsbStressTest ファイルは、ドライバーをインストールした後に、すべてのデータ転送のテストを実行します。</li>
</ul></td>
<td><p>usbstress.exe</p>
<p>usbstress.inf</p>
<p>usbstress.sys</p>
<p>UsbStressTest.bat</p></td>
</tr>
<tr class="odd">
<td><a href="muttutil.md" data-raw-source="[MuttUtil](muttutil.md)">MuttUtil</a></td>
<td><ul>
<li>テスト デバイスのファームウェアを更新します。</li>
<li>MUTT デバイス用のドライバーをインストールします。</li>
<li>デバイスがエラーなしにインストールされていることを確認します。</li>
<li>デバイスの動作のバス速度を変更します。</li>
<li>指定した期間後に再開ウェイク信号を送信するデバイスを構成します。</li>
<li>MUTT パックでは、完全なまたは高速度で動作するハブを設定します。としてシングル TT またはマルチ TT ハブです。</li>
</ul></td>
<td><p>MuttUtil.exe</p></td>
</tr>
<tr class="even">
<td><a href="how-to-retrieve-information-about-a-usb-device.md" data-raw-source="[USB hardware verifier](how-to-retrieve-information-about-a-usb-device.md)">USB ハードウェアの検証方法</a></td>
<td>コンソールで、ハードウェアのすべてのイベントを表示します。</td>
<td>USB3HWVerifierAnalyzer.exe</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB Test Tool (MUTT) デバイス](microsoft-usb-test-tool--mutt--devices.md)  




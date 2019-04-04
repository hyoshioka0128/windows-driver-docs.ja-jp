---
title: Windows Driver Kit のツールの索引
description: Windows Driver Kit のツールの索引
ms.assetid: 26db88c4-8fb8-4308-ab8a-1a1eef5e19d8
keywords:
- 支障をきたすかツール
- DbgCon ツール
- Sniffir ツール
- Sledge ツール
- 使用状況の検証ツールを呼び出す
- CUV ツール
- 示されているツールを WDK
- ドライバーの開発ツールを WDK を一覧表示
- スリープ状態の選択
- スリーパー
- Acpislp
- 手動の電源状態変更のテスト
- GUIDGen WDK
- WDK の GUID ジェネレーター
- GUIDGen.exe WDK
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: cac00eb60b57dee3eb425bfa6ec86f8c25abd7c3
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349559"
---
# <a name="index-of-windows-driver-kit-tools"></a>Windows Driver Kit のツールの索引


このトピックでは、Windows Driver Kit (WDK) に付属するツールについて基本的な情報を提供します。 このトピックでは、ドライバーの開発に役立つその他のツールへの参照も含まれています。 これらのツールは、使用可能なオペレーティング システムまたは個別のダウンロードとして使用できますがの一部として。 各ツールの詳細については、このトピックの「ツールの説明のドキュメントを参照してください。

最新の WDK を取得する方法については、[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=261797)を参照してください。

このトピックで、次のとおりです。

-   [ツールを WDK のインデックス](#index-of-wdk-tools)
-   [新機能については、WDK の Windows 8.1 です。](#what-s-new-in-the-wdk-for-windows8-1)
-   [Windows 8 向けの WDK の新機能新機能](#what-s-new-in-the-wdk-for-windows8)
-   [Windows 8 向けの WDK の変更点](#what-s-changed-in-the-wdk-for-windows8)
-   [サポートされているプラットフォーム](#supported-platforms)

### <a name="index-of-wdk-tools"></a>ツールを WDK のインデックス

次の表の情報には、Windows ドライバー開発者向けに利用できるツールについて説明します。 ツールの一覧には、WDK に付属するツールが含まれています (によって示される、 **WDK ツール**フィールド) もいくつかのツールは、Windows でインストールされるとは別に入手可能なまたは含まれています。 すべてのドライバーで一般的に使用できるツールについては、「[すべてのドライバー](#tech-all)します。 ツール、テクノロジに固有のグループ化は、たとえば、ツールは、固有の[Windows ポータブル デバイス (WPD) ドライバー](#tech-wpd)または[センサー](#tech-sensors)します。

-   [オーディオ/ビデオ ドライバー](#tech-audio-video)
-   [Bluetooth ドライバー](#tech-bluetooth)
-   [Windows Image Acquisition (WIA) ドライバー](#tech_wia)
-   [Windows ポータブル デバイス (WPD) ドライバー](#tech-wpd)
-   [プリンター ドライバー](#tech-printer)
-   [センサー](#tech-sensors)
-   [すべてのドライバー](#tech-all)

**注**  WindowsSdkDir %、Visual Studio 環境変数は、Windows キット ディレクトリに、WDK のこのバージョンがインストールされている例では、c: パスを表す\\Program Files (x86)\\Windows キット\\8.1。

 

### テクノロジ:オーディオ/ビデオ ドライバー <a name="tech-audio-video"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ツール名</th>
<th align="left">ツールの場所</th>
<th align="left">説明とヘルプ ファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>色の調整ツール (Dccw.exe) を表示します。</p>
<p><strong>WDK ツール:</strong>いいえ</p></td>
<td align="left"><p>%Windir%\System32\Dccw.exe</p></td>
<td align="left"><p>Windows と World Wide Web 国際標準赤、緑、青 (sRGB) に近い位置に、表示色を調整できるように調整ツール領域の色します。</p>
</tr>
<tr class="even">
<td align="left"><p>GraphEdt (Graphedt.exe)</p>
<p><strong>WDK のツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\graphedt.exe</p>
<p>%WindowsSdkDir%\tools\x64\graphedt.exe</p></td>
<td align="left"><p>ビルドには、ストリーミング オーディオ/ビデオ キャプチャ ドライバーをテストするグラフがフィルター処理します。</p>
<p>ドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=9230" data-raw-source="[Overview of GraphEdit](https://go.microsoft.com/fwlink/p/?linkid=9230)">GraphEdit の概要</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSStudio (KsStudio.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\KsStudio.exe</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.exe</p>
<div class="alert">
<strong>注</strong>  管理者特権を持っている人でこのツールを実行する必要があります。
</div>
<div>
 
</div></td>
<td align="left"><p>このツールは、フィルター グラフに表示されるフィルターとフィルターの内部ノード間の暗証番号 (pin)-pin 接続のグラフィカル表現を構築できます。</p>
<p>%WindowsSdkDir%\tools\x86\KsStudio.chm</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.chm</p>
<p>参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff554257" data-raw-source="[AVStream Testing and Debugging](https://msdn.microsoft.com/library/windows/hardware/ff554257)">AVStream テストおよびデバッグ</a>詳細についてはします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB デバイス ビューアー (Usbview.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Usbview.exe</p>
<p>%WindowsSdkDir%\tools\x64\Usbview.exe</p></td>
<td align="left"><p>USB ホスト コント ローラーと USB ハブ、および接続されている USB デバイスを列挙し、デバイスを USB 要求と、レジストリからデバイスに関する情報をクエリできます。</p>
<p>ソース コード参照の USB デバイスのビューアーは、コード ギャラリーからの<a href="https://go.microsoft.com/fwlink/p/?linkid=256205" data-raw-source="[USBVIEW Sample Application](https://go.microsoft.com/fwlink/p/?linkid=256205)">USBVIEW サンプル アプリケーション</a>します。</p></td>
</tr>
</tbody>
</table>

 

### テクノロジ:Bluetooth ドライバー <a name="tech-bluetooth"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ツール名</th>
<th align="left">ツールの場所</th>
<th align="left">説明とヘルプ ファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Bluetooth の照会レコードの検証ツール (Sdpverify.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Sdpverifiy.exe</p>
<p>%WindowsSdkDir%\tools\x64\Sdpverifiy.exe</p></td>
<td align="left"><p>Windows では解釈 Bluetooth デバイスの照会のレコードが表示されます。</p>
<p>WDK ドキュメント:</p>
<p><a href="bluetooth-inquiry-record-verifier.md" data-raw-source="[Bluetooth Inquiry Record Verifier](bluetooth-inquiry-record-verifier.md)">Bluetooth の照会レコード検証</a></p></td>
</tr>
</tbody>
</table>

 

### テクノロジ:Windows Image Acquisition (WIA) ドライバー<a name="tech_wia"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ツール名</th>
<th align="left">ツールの場所</th>
<th align="left">説明とヘルプ ファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIADbgCfg (Wiadbgcfg.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiadbgcfg.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.exe</p></td>
<td align="left"><p>WIA ドライバー (Windows Server 2008 および Windows の以降のバージョン) のログ記録を有効にします。</p>
<div class="alert">
<strong>注</strong>  以前のバージョンの Windows では、WIALogCfg を使用します。
</div>
<div>
 
</div>
<p>%WindowsSdkDir%\tools\x86\wiadbgcfg.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIAInfo2 (Wiainfo2.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiainfo2.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.exe</p></td>
<td align="left"><p>表示して、WIA デバイス ドライバーのプロパティを編集できるように、WIA 項目のツリーが表示されます。</p>
<p>%WindowsSdkDir%\tools\x86\wiainfo2.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIAPreview (Wiapreview.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiapreview.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.exe</p></td>
<td align="left"><p>WIA プレビュー コンポーネントとドライバーのセグメント化フィルターを使用する方法を示します。</p>
<p>%WindowsSdkDir%\tools\x64\wiapreview.htm</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIATest (Wiatest.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiatest.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiatest.exe</p></td>
<td align="left"><p>ドライバー、ドライバー、および各プロパティの現在の値によって公開される Windows Image Acquisition (WIA) プロパティによって作成される項目のツリーが表示されます。 このツールを使用して、開発と単体テストの中に、ドライバーをデバッグすることができます。</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Imaging トレース ファイル ビューアー (Wiatrcvw.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\Wiatrcvw.exe</p>
<p>%WindowsSdkDir%\tools\x86\Wiatrcvw.exe</p></td>
<td align="left"><p>WIA トレース ログ (%windir%\debug\wia\wiatrace.log) を表示し、各モジュールの WIA トレース パラメーターを変更することができます。</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p></td>
</tr>
</tbody>
</table>

 

### テクノロジ:Windows ポータブル デバイス (WPD) ドライバー <a name="tech-wpd"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ツール名</th>
<th align="left">ツールの場所</th>
<th align="left">説明とヘルプ ファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WpdDeviceInspector (WpdDeviceInspector.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdDeviceInspector.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdDeviceInspector.exe</p></td>
<td align="left"><p>WPD ドライバーをクエリし、デバイスとその機能を説明する包括的な HTML レポートを生成します。 たとえば、サポートされているデバイスのコマンドとオブジェクトの一覧を取得するのに使用できます。 また、このツールの各オブジェクトでサポートされるすべてのプロパティのリストが生成されます。</p>
<p>WDK ドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows ポータブル デバイス</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD ドライバーの開発ツール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WpdInfo (WpdInfo.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdInfo.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdInfo.exe</p></td>
<td align="left"><p>などの一般的な WPD 操作を実行します: を開くと、デバイスを閉じて、作成または、デバイス上のオブジェクトを削除するおよびデバイス コマンドを発行します。</p>
<p>WDK ドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows ポータブル デバイス</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD ドライバーの開発ツール</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft Network Monitor (NetMon.exe)</p>
<p><strong>WDK ツール:</strong>いいえ</p></td>
<td align="left"><p>Microsoft ネットワーク モニターをダウンロード (NetMon.exe<a href="https://go.microsoft.com/fwlink/p/?linkid=248501" data-raw-source="[here](https://go.microsoft.com/fwlink/p/?linkid=248501)">ここ</a>します。</p></td>
<td align="left"><p>WPD コンポーネントからの情報のトレースが表示されます。 このツールには、以前のバージョンの WDK で提供されていたいる WpdMon.exe が置き換えられます。</p>
<p>WDK ドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows ポータブル デバイス</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD ドライバーの開発ツール</a>を参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/hh451296" data-raw-source="[Using the Network Monitor Tool](https://msdn.microsoft.com/library/windows/hardware/hh451296)">ネットワーク監視ツールを使用して</a>します。</p></td>
</tr>
</tbody>
</table>

 

### テクノロジ:プリンター ドライバー <a name="tech-printer"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ツール名</th>
<th align="left">ツールの場所</th>
<th align="left">説明とヘルプ ファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GPDCheck (Gpdcheck.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\gpdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\gpdcheck.exe</p></td>
<td align="left"><p>構文の正確さの汎用的なプリンターの説明ファイル (GPD) を検証します。</p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>gpdcheck/でしょうか。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>INFGate (Infgate.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\infgate.exe</p>
<p>%WindowsSdkDir%\tools\x86\infgate.exe.exe</p></td>
<td align="left"><p>プリンターの INF ファイルの準拠を検証します。</p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>infgate /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>isxps 適合 (isXPS.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\isxps\isxps.exe</p>
<p>%WindowsSdkDir%\tools\x86\isxps\isxps.exe</p></td>
<td align="left"><p>XPS および OPC 仕様に XPS ファイルの準拠を検証します。</p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>isxps 適合/でしょうか。</strong> コマンド プロンプト ウィンドウでします。</p>
<p>詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=150004" data-raw-source="[isXPS Conformance Tool](https://go.microsoft.com/fwlink/p/?linkid=150004)">isxps 適合性ツール</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Looksgood (Looksgood.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\looksgood.exe</p>
<p>%WindowsSdkDir%\tools\x86\looksgood.exe</p></td>
<td align="left"><p>XPS のレンダリング エンジンの正確性を検証します。</p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>looksgood /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeNTF (Makentf.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\makentf.exe</p>
<p>%WindowsSdkDir%\tools\x86\makentf.exe</p></td>
<td align="left"><p>Adobe フォント メトリック (して) および東アジア フォント AFM ファイルを Windows フォント ファイル (.ntf) に変換します。</p>
<p>WDK ドキュメント:</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546364" data-raw-source="[Converting AFM Files to NTF Files](https://msdn.microsoft.com/library/windows/hardware/ff546364)">NTF ファイルに変換します。</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546366" data-raw-source="[Converting East Asian AFM Files to NTF Files](https://msdn.microsoft.com/library/windows/hardware/ff546366)">東アジアしてを NTF ファイルに変換します。</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PPDCheck (Ppdcheck.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ppdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\ppdcheck.exe</p></td>
<td align="left"><p>PostScript プリンター説明ファイル (PPD) の構文の正確さを検証します。</p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>ppdcheck/でしょうか。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PTConform (PTConform.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PTConform.exe</p>
<p>%WindowsSdkDir%\tools\x86\PTConform.exe</p></td>
<td align="left"><p>印刷スキーマに適合する印刷チケットまたは印刷機能のドキュメントを検証します。</p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>ptconform/でしょうか。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>XpsAnalyzer (XpsAnalyzer.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\XpsAnalyzer.exe</p>
<p>%WindowsSdkDir%\tools\x86\XpsAnalyzer.exe</p></td>
<td align="left"><p>XPS 1.0 仕様と互換性のための XML Paper Specification (XPS) ファイルを分析します。</p>
<p>WDK ドキュメント:</p>
<p><a href="xpsanalyzer.md" data-raw-source="[XpsAnalyzer](xpsanalyzer.md)">XpsAnalyzer</a></p></td>
</tr>
</tbody>
</table>

 

### テクノロジ:センサー <a name="tech-sensors"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ツール名</th>
<th align="left">ツールの場所</th>
<th align="left">説明とヘルプ ファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>センサー診断ツール (sensordiagnostictool.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>ドライバー、ファームウェア、およびハードウェア センサーと場所の機能をテストします。 ツールは、データの取得、イベント処理、レポートの間隔をテストするには、プロパティの取得の秘密度を変更するには、センサーと API の場所を呼び出します。</p>
<p>WDK ドキュメント:</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh780319" data-raw-source="[Testing sensor functionality with the Sensor Diagnostic Tool](https://msdn.microsoft.com/library/windows/hardware/hh780319)">センサー診断ツールを使用したセンサー機能をテストします。</a></p></td>
</tr>
</tbody>
</table>

 

### テクノロジ:すべてのドライバー <a name="tech-all"></a>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ツール名</th>
<th align="left">ツールの場所</th>
<th align="left">説明とヘルプ ファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BinPlace (Binplace.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\binplace.exe</p></td>
<td align="left"><p>管理大きなファイルを移動することによってプロジェクトのコーディングから実行可能ファイル、シンボルを抽出およびからプライベート シンボルを削除するシンボル ファイル。</p>
<p>WDK ドキュメント:</p>
<p><a href="binplace.md" data-raw-source="[BinPlace](binplace.md)">BinPlace</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバーのコード分析</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>Visual Studio でコード分析ツールが含まれます。 ドライバー固有のコンポーネントは、WDK をインストールするときに追加されます。</p></td>
<td align="left"><p>C および C++ コーディング エラーを検出する静的検証ツールです。 このバージョンは具体的には、カーネル モード ドライバーにはエラーを検出するために設計されています。</p>
<div class="alert">
<strong>注</strong>  WDK の以前のバージョンでこの機能は OACR の一部であった、スタンドアロン ツール: PREfast for Drivers としてもありました。 Visual Studio 2012 以降では、Visual Studio に機能が統合されました。
</div>
<div>
 
</div>
<p>WDK ドキュメント:</p>
<p><a href="code-analysis-for-drivers.md" data-raw-source="[Code Analysis for Drivers](code-analysis-for-drivers.md)">ドライバーのコード分析</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>CertMgr (CertMgr.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\CertMgr.exe</p>
<p>%WindowsSdkDir%\bin\x86\CertMgr.exe</p></td>
<td align="left"><p>管理証明書信頼リスト (Ctl) を証明書および証明書の失効リスト (Crl) ドライバーの署名に使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver packages](https://msdn.microsoft.com/library/windows/hardware/ff544840)">ドライバー パッケージ</a>します。</p>
<p>WDK ドキュメント:</p>
<p><a href="certmgr.md" data-raw-source="[&lt;strong&gt;CertMgr&lt;/strong&gt;](certmgr.md)"><strong>CertMgr</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ChkINF</p>
<p><strong>WDK ツール:</strong>非推奨</p></td>
<td align="left"><p>前のパス:</p>
<p>%WindowsSdkDir%\tools\x86\Chkinf</p></td>
<td align="left"><p>ChkInf は非推奨とされました。 代わりに、 <a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p>
<p>WDK ドキュメント:</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>コンピューター ハードウェア識別ツール (ComputerHardwareIds.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p><strong>Windows Driver Kit (WDK) 8:</strong></p>
<p>%WindowsSdkDir%\tools\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\tools\x86\ComputerHardwareIds.exe</p>
<p>WDKPath\tools\Other\ia64\ComputerHardwareIds.exe</p>
<p><strong>Windows Driver Kit (WDK) 8.1:</strong></p>
<p>%WindowsSdkDir%\bin\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\x86\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\arm\ComputerHardwareIds.exe</p></td>
<td align="left"><p>コンピューターのハードウェア Id を SMBIOS 情報から派生します。</p>
<p>WDK ドキュメント:</p>
<p><a href="computerhardwareids.md" data-raw-source="[ComputerHardwareIds](computerhardwareids.md)">ComputerHardwareIds</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DC2WMIParser (DC2WMIParser.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\DC2WMIParser.exe</p>
<p>%WindowsSdkDir%\tools\x86\DC2WMIParser.exe</p></td>
<td align="left"><p>DC2WMIParser は、Driver Verifier で作成される WMI IRP のレコードを収集するツールは、このログをテキスト ファイルに変換します。</p>
<p>ドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=698758" data-raw-source="[IRP Logging](https://go.microsoft.com/fwlink/p/?LinkId=698758)">IRP ログ</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Dependency Walker (Depends.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\depends.exe</p>
<p>%WindowsSdkDir%\tools\x86\depends.exe</p></td>
<td align="left"><p>ツリー ダイアグラム内のアプリケーションで必要なモジュールの依存関係パターンが表示されます。 関数が呼び出した他のモジュールでは、実際には、各モジュールによってエクスポートされた関数を含む、多数の詳細が含まれ、モジュールの読み込みと実行に必要なファイルの最小値を設定します。</p>
<p>ツールから、 <strong>Dependency Walker</strong>ヘルプ メニューの <strong>ヘルプ トピック</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DevCon (Devcon.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p></td>
<td align="left"><p>デバイス マネージャーのコマンド ライン バージョン。 DevCon によりを無効にします、インストール、構成、および、ローカル コンピューター上のデバイスを削除しますおよびローカルおよびリモート コンピューター上のデバイスの詳細情報を表示します。</p>
<p>WDK ドキュメント:</p>
<p><a href="devcon.md" data-raw-source="[DevCon](devcon.md)">DevCon</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ドライバー (Drivers.exe:)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\drivers.exe</p>
<p>%WindowsSdkDir%\tools\x86\drivers.exe</p></td>
<td align="left"><p>コンピューターにインストールされているすべてのドライバーの一覧が表示されます。</p>
<p>WDK ドキュメント:</p>
<p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>Driver Verifier (Verifier.exe)</p>
<p><strong>WDK ツール:</strong>いいえ</p></td>
<td align="left"><p>%Windir%\system32\verifier.exe</p></td>
<td align="left"><p>モニターのカーネル モード ドライバーとグラフィック ドライバーを無効な関数呼び出しまたはシステムが破損する可能性がありますアクションを検出します。 負荷と不適切な動作を検索するテストのさまざまなドライバーを対象にできます。</p>
<p>WDK ドキュメント:</p>
<p><a href="driver-verifier.md" data-raw-source="[Driver Verifier](driver-verifier.md)">ドライバーの検証ツール</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ドライバー検証ログ (DVL)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>Microsoft Visual Studio および WDK が必要です。 <strong>ドライバー</strong>  メニューのをクリックして<strong>ドライバー検証ログを作成しています.</strong></p></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=227016" data-raw-source="[Windows Server 2012 Hardware Certification Program](https://go.microsoft.com/fwlink/p/?linkid=227016)">Windows Server 2012 のハードウェア認定プログラム</a>ドライバー検証ログ (DVL) 該当するドライバーのすべての要求送信が必要です。 DVL には、コード分析と静的ドライバー検証ツールのログ ファイルからの結果の要約が含まれています。 参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_verification_log" data-raw-source="[Creating a Driver Verification Log](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_verification_log)">ドライバー検証ログを作成する</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>拡張記憶域証明書管理ツール (EhStorCertMgrCmd.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ehstorcertmgrcmd.exe</p>
<p>%WindowsSdkDir%\tools\x86\ehstorcertmgrcmd.exe</p></td>
<td align="left"><p>標準的な IEEE 1667 に対応している USB ストレージ デバイスに証明書を管理します。</p>
<p>WDK ドキュメント:</p>
<p><a href="enhanced-storage-certificate-management-tool.md" data-raw-source="[Enhanced Storage Certificate Management Tool](enhanced-storage-certificate-management-tool.md)">拡張記憶域証明書の管理ツール</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>イベントとパフォーマンス カウンター マニフェスト ジェネレーター ツール (ECManGen.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\ECManGen.exe</p>
<p>%WindowsSdkDir%\bin\x86\ECManGen.exe</p></td>
<td align="left"><p>イベントまたはパフォーマンスのカウンター マニフェストを作成するためのツール (* .man) XML を使用することがなく最初からタグを付けます。 マニフェスト ファイルを作成する方法の詳細については、<a href="https://msdn.microsoft.com/library/windows/desktop/dd996930" data-raw-source="[Writing an Instrumentation Manifest (Windows)](https://msdn.microsoft.com/library/windows/desktop/dd996930)">インストルメンテーション マニフェスト (Windows) を記述</a>セクションと<a href="adding-event-tracing-to-kernel-mode-drivers.md" data-raw-source="[Adding Event Tracing to Kernel-Mode Drivers](adding-event-tracing-to-kernel-mode-drivers.md)">カーネル モード ドライバーへのイベント トレースの追加</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUIDgen (Guidgen.exe)</p>
<p><strong>WDK ツール:</strong>いいえ</p></td>
<td align="left"><p>ダウンロードから入手できる<a href="https://go.microsoft.com/fwlink/p/?linkid=121586" data-raw-source="[Microsoft Exchange Server GUID Generator](https://go.microsoft.com/fwlink/p/?linkid=121586)">Microsoft Exchange Server GUID ジェネレーター</a></p></td>
<td align="left"><p>クラス、オブジェクト、およびインターフェイスを識別するために使用できるグローバル一意識別子 (GUID) を生成します。 生成された GUID は、ソース コードに挿入できるように、4 つの形式のいずれかでクリップボードにコピーされます。</p>
<p>GUIDGEN.doc (ダウンロード パッケージに含まれています)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Inf2Cat (Inf2cat.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\inf2cat.exe</p>
<p>%WindowsSdkDir%\bin\x86\inf2cat.exe</p></td>
<td align="left"><p>決定かどうかを<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver package's](https://msdn.microsoft.com/library/windows/hardware/ff544840)">ドライバー パッケージの</a>INF ファイルは、の Windows バージョンでは、指定されたリストのデジタル署名することができ、そうである場合は、符号なし生成します<a href="https://msdn.microsoft.com/library/windows/hardware/ff537872" data-raw-source="[catalog files](https://msdn.microsoft.com/library/windows/hardware/ff537872)">カタログ ファイル</a>指定の Windows に適用します。バージョン。</p>
<p>WDK ドキュメント:</p>
<p><a href="inf2cat.md" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](inf2cat.md)"><strong>Inf2Cat</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>InfVerif (InfVerif.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>c:\Program Files(x86)\Windows Kits\10\tools\arm\infverif.exe</p>
<p>c:\Program Files(x86)\Windows Kits\10\tools\arm64\infverif.exe</p>
<p>c:\Program Files(x86)\Windows Kits\10\tools\x86\infverif.exe</p>
<p>c:\Program Files(x86)\Windows Kits\10\tools\x64\infverif.exe</p>
<td align="left"><p>ドライバーの INF ファイルをテストします。 INF 構文の問題の報告、だけでなく、ツールは、INF ファイルがユニバーサルを報告します。</p>
<p>WDK ドキュメント:</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p></td>
</tr>

<tr class="even">
<td align="left"><p>MakeCat (MakeCat.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>WDKPath\bin\amd64\MakeCat.exe</p>
<p>WDKPath\bin\ia64\MakeCat.exe</p>
<p>WDKPath\bin\x86\MakeCat.exe</p></td>
<td align="left"><p>作成、<a href="https://msdn.microsoft.com/library/windows/hardware/ff537872" data-raw-source="[catalog file](https://msdn.microsoft.com/library/windows/hardware/ff537872)">カタログ ファイル</a>の<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver package](https://msdn.microsoft.com/library/windows/hardware/ff544840)">ドライバー パッケージ</a>します。</p>
<p>WDK ドキュメント:</p>
<p><a href="makecat.md" data-raw-source="[MakeCat](makecat.md)">MakeCat</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeCert (MakeCert.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\MakeCert.exe</p>
<p>%WindowsSdkDir%\bin\x86\MakeCert.exe</p></td>
<td align="left"><p>システム テストのルート キーによって、または別の指定したキーによって署名された X.509 証明書を作成します。</p>
<p>WDK ドキュメント:</p>
<p><a href="makecert.md" data-raw-source="[&lt;strong&gt;MakeCert&lt;/strong&gt;](makecert.md)"><strong>MakeCert</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>MSBuild (MSBuild.exe)</p>
<p><strong>WDK ツール:</strong>いいえ</p></td>
<td align="left"><p>Visual Studio と共にインストール</p></td>
<td align="left"><p>サンプル、ドライバー、および Microsoft WDK で指定される関連するソフトウェア コンポーネントをビルドします。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262804" data-raw-source="[MSBuild]( https://go.microsoft.com/fwlink/p/?linkid=262804)">MSBuild</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PnpCpu (PnPCpu.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PnPCpu.exe</p>
<p>%WindowsSdkDir%\tools\x86\PnPCpu.exe</p></td>
<td align="left"><p>Windows Server 2008 のインスタンスを実行するプロセッサのホット追加をシミュレートします。</p>
<p>WDK ドキュメント:</p>
<p><a href="pnpcpu.md" data-raw-source="[PNPCPU](pnpcpu.md)">PNPCPU</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PnPUtil (PnPUtil.exe)</p>
<p><strong>WDK ツール:</strong>いいえ</p></td>
<td align="left"><p>%Windir%\system32\pnputil.exe</p></td>
<td align="left"><p>コマンド ライン ツールをインストールまたは削除する<a href="https://msdn.microsoft.com/library/windows/hardware/ff544840" data-raw-source="[driver packages](https://msdn.microsoft.com/library/windows/hardware/ff544840)">ドライバー パッケージ</a>Windows ドライバー ストアから。</p>
<p>このツールは、Windows 7 および Windows の以降のバージョンで使用できます。</p>
<p>WDK ドキュメント:</p>
<p><a href="pnputil.md" data-raw-source="[PnPUtil](pnputil.md)">PnPUtil</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PoolMon (Poolmon.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\poolmon.exe</p>
<p>%WindowsSdkDir%\tools\x86\poolmon.exe</p></td>
<td align="left"><p>オペレーティング システムがメモリの割り当てについて、システムのページおよび非ページ カーネル プール、およびターミナル サービス セッションに使用されるメモリ プールから収集するデータを表示します。 データは、プール割り当てタグでグループ化されます。</p>
<p>WDK ドキュメント:</p>
<p><a href="poolmon.md" data-raw-source="[PoolMon](poolmon.md)">PoolMon</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PowerCfg (PowerCfg.exe)</p>
<p><strong>WDK ツール:</strong>いいえ</p></td>
<td align="left"><p>%Windir%\system32\powercfg.exe</p></td>
<td align="left"><p>コマンド ライン ツールには、システムのエネルギー効率の評価に使用されます。</p>
<p>このツールは、Windows 7 および Windows の以降のバージョンで使用できます。</p>
<p>デベロッパー センターのドキュメント:</p>
<a href="http://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx" data-raw-source="[Using PowerCfg to Evaluate System Energy Efficiency](http://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx)">システムのエネルギー効率の評価に PowerCfg を使用</a>
<p>コマンド オプションについては、次のように入力します。</p>
<p></p>
<p><strong>PowerCfg /?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Pvk2Pfx (Pvk2Pfx.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\Pvk2Pfx.exe</p>
<p>%WindowsSdkDir%\bin\x86\Pvk2Pfx.exe</p></td>
<td align="left"><p>コピーの公開キーと秘密キーの情報、personal information exchange (.pfx) ファイルに .spc、.cer、.pvk ファイルに含まれています。</p>
<p>WDK ドキュメント:</p>
<p><a href="pvk2pfx.md" data-raw-source="[&lt;strong&gt;Pvk2Pfx&lt;/strong&gt;](pvk2pfx.md)"><strong>Pvk2Pfx</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PwrTest (Pwrtest.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\pwrtest.exe</p>
<p>%WindowsSdkDir%\tools\x86\pwrtest.exe</p></td>
<td align="left"><p>電源管理ツール Windows 7 以降を実行して、レコードの電源管理コンピューターから情報。</p>
<p>WDK ドキュメント:</p>
<p><a href="pwrtest.md" data-raw-source="[PwrTest](pwrtest.md)">PwrTest</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SignTool (SignTool.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\SignTool.exe</p>
<p>%WindowsSdkDir%\bin\x86\SignTool.exe</p></td>
<td align="left"><p>デジタル署名ファイル、ファイル、およびファイルにタイムスタンプの署名を検証します。</p>
<p>WDK ドキュメント:</p>
<p><a href="signtool.md" data-raw-source="[&lt;strong&gt;SignTool&lt;/strong&gt;](signtool.md)"><strong>SignTool</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Stampinf (Stampinf.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\stampinf.exe</p>
<p>%WindowsSdkDir%\bin\x86\stampinf.exe</p></td>
<td align="left"><p>更新を含む共通の INF ファイル ディレクティブ、 <strong>DriverVer</strong>ディレクティブ。</p>
<p>WDK ドキュメント:</p>
<p><a href="stampinf.md" data-raw-source="[Stampinf](stampinf.md)">Stampinf</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>静的ドライバー検証ツール</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\SDV</p>
<p></p>
<div class="alert">
<strong>注</strong>  からの Static Driver Verifier の起動、<strong>ドライバー</strong> Visual Studio のメニュー。
</div>
<div>
 
</div></td>
<td align="left"><p>体系的に Windows ドライバーのソース コードを分析して、Windows オペレーティング システムのカーネルのドライバーが正しく対話するかどうかを決定する静的検証ドライバー ツール。</p>
<p>WDK ドキュメント:</p>
<p><a href="static-driver-verifier.md" data-raw-source="[Static Driver Verifier](static-driver-verifier.md)">静的ドライバー検証ツール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Tracefmt (Tracefmt.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracefmt.exe</p></td>
<td align="left"><p>書式設定し、イベント トレース ログ ファイル (.etl) またはリアルタイムのトレース セッションからのトレース メッセージを表示します。</p>
<p>WDK ドキュメント:</p>
<p><a href="tracefmt.md" data-raw-source="[Tracefmt](tracefmt.md)">Tracefmt</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>TraceLog (Tracelog.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p><strong>WDK 8:</strong></p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>WDK 8.1:</strong></p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\arm\tracelog.exe</p></td>
<td align="left"><p>構成し、コマンドラインからトレース セッションを制御します。 遅延プロシージャに費やされた時間を計測呼び出し (Dpc) および割り込みサービス ルーチン (Isr)。</p>
<p>WDK ドキュメント:</p>
<p><a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">トレース ログ</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TracePDB (Tracepdb.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracepdb.exe</p></td>
<td align="left"><p>WPP トレース プロバイダーの完全なまたはプライベートの PDB シンボル ファイルのトレース メッセージの形式 (.tmf) ファイルを作成します。</p>
<p>WDK ドキュメント:</p>
<p><a href="tracepdb.md" data-raw-source="[Tracepdb](tracepdb.md)">Tracepdb</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Traceview で (Traceview.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\TraceView.exe</p>
<p>%WindowsSdkDir%\tools\x86\TraceView.exe</p></td>
<td align="left"><p>構成しトレース セッションを制御し、リアルタイムのトレース セッションとトレース ログから書式設定済みトレース メッセージが表示されます。 Traceview では、グラフィック ユーザー インターフェイスとバッチ処理と、スクリプトのコマンド ライン インターフェイスを持ちます。</p>
<p>WDK ドキュメント:</p>
<p><a href="traceview.md" data-raw-source="[TraceView](traceview.md)">Traceview で</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TraceWPP (Tracewpp.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracewpp.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracewpp.exe</p></td>
<td align="left"><p>Windows ソフトウェア トレース プリプロセッサ (WPP) を実行します。</p>
<p>WDK ドキュメント:</p>
<p><a href="wpp-preprocessor.md" data-raw-source="[WPP Preprocessor](wpp-preprocessor.md)">WPP プリプロセッサ</a></p>
<p><a href="survey-of-software-tracing-tools.md" data-raw-source="[Survey of Software Tracing Tools](survey-of-software-tracing-tools.md)">ソフトウェア トレース ツールのアンケート</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WDF のテスト担当者</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>一連のテスト、検証、およびドライバーを WDF のデバッグに使用できるツール。 ツールセットは、スクリプトまたはコンパイル済みのアプリケーションで使用できる WMI のプログラミング インターフェイスを提供します。</p>
<p>WDK ドキュメント:</p>
<p><a href="wdftester--wdf-driver-testing-toolset.md" data-raw-source="[WdfTester: WDF Driver Testing Toolset](wdftester--wdf-driver-testing-toolset.md)">WdfTester:WDF ドライバー テスト ツールセット</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WDF Verifier (Wdfverifier.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wdfverifier.exe</p>
<p>%WindowsSdkDir%\tools\x86\wdfverifier.exe</p></td>
<td align="left"><p>KMDF および UMDF ドライバーのフレームワークの検証方法を使いやすいインターフェイスを提供します。</p>
<p>WDK ドキュメント:</p>
<p><a href="wdf-verifier-control-application.md" data-raw-source="[WDF Verifier Control Application](wdf-verifier-control-application.md)">WDF Verifier コントロール アプリケーション</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>(WSD) の基本的な相互運用性ツール (WSDBIT) デバイスで web サービスします。</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p><strong>WSDBIT クライアント:</strong></p>
<p>%WindowsSdkDir%\tools\x64\wsdbit_client.exe</p>
<p>%WindowsSdkDir%\tools\x86\wsdbit_client.exe</p>
<p><strong>WSDBIT サーバー:</strong></p>
<p>%WindowsSdkDir%\tools\x64\wsdbit_server.exe</p>
<p>%WindowsSdkDir%\tools\x86\wsdbit_server.exe</p></td>
<td align="left"><p>実装を確認します。<a href="https://go.microsoft.com/fwlink/p/?linkid=81255" data-raw-source="[Device Profile for Web Services (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)">デバイス プロファイルの Web サービス (DPWS)</a> WSDAPI で動作します。</p>
<p>WDK ドキュメント:</p>
<p><a href="wsdapi-basic-interoperability-tool.md" data-raw-source="[WSD Interoperability Tool](wsdapi-basic-interoperability-tool.md)">WSD 相互運用性ツール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Winerror (Winerror.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\winerror.exe</p>
<p>%WindowsSdkDir%\tools\x86\winerror.exe</p></td>
<td align="left"><p>指定したエラー (Winerror.h) または成功コード (Ntstatus.h) のエラー メッセージ識別子とマッピング情報を返します。</p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>winerror/でしょうか。</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WMIMofCk (Wmimofck.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\wmimofck.exe</p></td>
<td align="left"><p>WDK ドキュメント:</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565588" data-raw-source="[Using wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)">Wmimofck.exe を使用します。</a></p>
<p>コマンド オプションについては、次のように入力します。</p>
<p><strong>wmimofck -?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>WsdCodeGen (Wsdcodegen.exe)</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\wsdcodegen.exe</p>
<p>%WindowsSdkDir%\bin\x86\wsdcodegen.exe</p></td>
<td align="left"><p>プロキシとスタブ Web サービス コントラクトに基づいて自動的に生成します。 主に、このツールを使用すると、クライアント アプリケーションを作成します。 ただし、テスト用またはユーザー モード ドライバーを作成するために使用することができます。</p>
<p>クラス、プロパティ、メソッド、およびバイナリの MOF ファイル (.bmf) で指定されたイベントが WMI の使用に対して有効であることを検証します。 サポートの MOF ファイルを生成します。</p>
<p>Windows SDK:</p>
<p>参照してください、 <a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">Web Services on Devices</a>セクション</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WSDDebug_client と WSDDebug_host</p>
<p><strong>WDK ツール:</strong>はい</p></td>
<td align="left"><p><strong>クライアントをデバッグするには。</strong></p>
<p>%WindowsSdkDir%\bin\x64\WSDDebug_client.exe</p>
<p>%WindowsSdkDir%\bin\x86\WSDDebug_client.exe</p>
<p><strong>ホストをデバッグするには。</strong></p>
<p>%WindowsSdkDir%\bin\x64\WSDDebug_host.exe</p>
<p>%WindowsSdkDir%\bin\x86\WSDDebug_host.exe</p></td>
<td align="left"><p>これらのツールは、論理デバイスとデバイスまたはアプリケーションのトラブルシューティングに使用できるクライアントは。</p>
<p>Windows SDK:</p>
<p>参照してください、 <a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">Web Services on Devices</a>セクション</p></td>
</tr>
</tbody>
</table>

 

### 新機能については、WDK の Windows 8.1 です。 <a name="what-s-new-in-the-wdk-for-windows8-1"></a>

次のツールが追加されましたまたは WDK 8.1 で変更されています。

-   HCK のテスト スイート (を参照してください[Visual Studio を使用して実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)と[WDK 8.1 では、HCK のテスト スイートを実行する方法](https://msdn.microsoft.com/windows-drivers/develop/run_the_hck_test_suites_in_the_wdk))。

-   [Driver Verifier](driver-verifier.md)— Windows ドライバーでエラーを検出するための 4 つの新しいオプションになりました。
-   [PwrTest](pwrtest.md): ドキュメントについては、スタンバイ電源状態の接続のサポートを含む、新しいテストのシナリオを更新します。
-   [Tracelog](tracelog.md)-新しいオプション。

### Windows 8 向けの WDK の新機能新機能 <a name="what-s-new-in-the-wdk-for-windows8"></a>

For Windows 8 WDK には、次のツールが追加されました。

-   Bluetooth の照会レコードの検証ツール (Sdpverify.exe)

-   デバイスの基本テスト (を参照してください[Visual Studio を使用して実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)と[を選択して、デバイスの基本テストを構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)します。

-   センサー診断ツール (sensordiagnostictool.exe)

### Windows 8 向けの WDK の変更点 <a name="what-s-changed-in-the-wdk-for-windows8"></a>
次のツールでは、Windows 7 では、Microsoft の WDK に含まれていたが、for Windows 8 WDK には含まれません。

-   Windows 生体認証フレームワーク ツール (BioTest.exe、WBDIDriverTest.exe)

-   デバイス パス Exerciser (devpathexer.exe)。 基本的なデバイスの一員となったはファジー テストです。

-   IoSpy と IoAttack (IoSpyCmd.exe、IoAttack.exe)。 基本的なデバイスの一員となったをテストします。

-   Kernrate (Kernrate.exe) Kernrate がサポートされていません。 代わりに、使用、 [Windows Performance Analysis Toolkit](https://go.microsoft.com/fwlink/p/?linkid=294280)します。

-   自動コード レビュー (OACR) (ドライバー コンポーネント今部分の Visual Studio でコード分析ツールです。)

-   プラグ アンド プレイ ドライバーのテスト (pnpdtest.exe)。 基本的なデバイスの一員となったをテストします。

-   ProCalc

-   WWAN ドライバー テスト アプリ (wwandrivertestapp.exe)

### <a name="supported-platforms"></a>サポートされているプラットフォーム

WDK 8.1 には、これらのバージョンの Windows で実行されるドライバーの開発がサポートされています。

-   Windows 8.1 および Windows 8

-   Windows Server 2012 R2 および Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

-   (SP1 と SP2 含む)、Windows Vista WDK 8 を使用する必要があります。 Windows xp では、WDK 7 を使用する必要があります。

これらのバージョンの Windows では、統合された Visual Studio ドライバーの開発環境を実行できます。

-   Windows 8.1 および Windows 8

-   Windows Server 2012 R2 および Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

 

 


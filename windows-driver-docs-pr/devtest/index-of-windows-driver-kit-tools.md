---
title: Windows Driver Kit のツールの索引
description: Windows Driver Kit のツールの索引
ms.assetid: 26db88c4-8fb8-4308-ab8a-1a1eef5e19d8
keywords:
- Disabler ツール
- DbgCon ツール
- Sniffir ツール
- Sledge ツール
- 使用状況検証ツールの呼び出し
- CUV ツール
- ツール WDK、一覧
- ドライバー開発ツール WDK、一覧
- スリープ状態の選択
- sleeper
- Acpislp
- 手動による電源状態の変更テスト
- Guidgen.exe WDK
- GUID ジェネレーター WDK
- Guidgen.exe WDK
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33cdaf80ef88dd61f3f8c1971366bc7a0058ce0d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209458"
---
# <a name="index-of-windows-driver-kit-tools"></a>Windows Driver Kit のツールの索引


このトピックでは、Windows Driver Kit (WDK) に含まれるツールに関する基本的な情報を提供します。 このトピックには、ドライバーの開発に役立つその他のツールへの参照も含まれています。 これらの他のツールは、オペレーティングシステムの一部として使用することも、個別のダウンロードとして入手することもできます。 各ツールの詳細については、このトピックのツールに関するドキュメントを参照してください。

最新の WDK を入手する方法については、「 [Windows Driver Kit (wdk)](https://go.microsoft.com/fwlink/p/?linkid=261797)」を参照してください。

このトピックの内容は次のとおりです。

-   [WDK ツールのインデックス](#index-of-wdk-tools)
-   [WDK for Windows 8.1 の新機能](#what-s-new-in-the-wdk-for-windows8-1)
-   [Windows 8 用 WDK の新機能](#what-s-new-in-the-wdk-for-windows8)
-   [Windows 8 用 WDK の変更点](#what-s-changed-in-the-wdk-for-windows8)
-   [サポートされているプラットフォーム](#supported-platforms)

### <a name="index-of-wdk-tools"></a>WDK ツールのインデックス

次の表の情報は、Windows ドライバー開発者に役立つツールについて説明しています。 ツールの一覧には、WDK に付属するツール ( **wdk ツール**フィールドによって示される) が含まれています。また、個別に利用できるツールや、Windows と共にインストールされるツールも含まれています。 すべてのドライバーで一般的に使用できるツールは、[すべて](#tech-all)のドライバーの下に一覧表示されます。 テクノロジに固有のツールは、 [Windows ポータブルデバイス (WPD) ドライバー](#tech-wpd)や[センサー](#tech-sensors)に固有のツールなど、グループ化されています。

-   [オーディオ/ビデオドライバー](#tech-audio-video)
-   [Bluetooth ドライバー](#tech-bluetooth)
-   [Windows イメージ取得 (WIA) ドライバー](#tech_wia)
-   [Windows ポータブルデバイス (WPD) ドライバー](#tech-wpd)
-   [プリンタードライバー](#tech-printer)
-   [センサー](#tech-sensors)
-   [すべてのドライバー](#tech-all)

**注**  Visual Studio 環境変数% WindowsSdkDir% は、このバージョンの WDK がインストールされている windows kit ディレクトリへのパスを表します。たとえば、C:\\Program Files (x86)\\windows kit\\8.1 です。

 

### テクノロジ: オーディオ/ビデオドライバー<a name="tech-audio-video"></a>

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
<th align="left">説明とヘルプファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>カラー調整ツール (Dccw .exe) を表示する</p>
<p><strong>WDK ツール:</strong>違います</p></td>
<td align="left"><p>%Windir%\System32\Dccw.exe</p></td>
<td align="left"><p>調整ツール。ユーザーが表示色を調整して、Windows および World Wide Web 国際標準の赤と青 (sRGB) の色空間に近づけることができます。</p>
</tr>
<tr class="even">
<td align="left"><p>GraphEdt (Graphedt)</p>
<p><strong>WDK のツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\graphedt.exe</p>
<p>%WindowsSdkDir%\tools\x64\graphedt.exe</p></td>
<td align="left"><p>フィルターグラフをビルドして、ストリーミングオーディオ/ビデオキャプチャドライバーをテストします。</p>
<p>書</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=9230" data-raw-source="[Overview of GraphEdit](https://go.microsoft.com/fwlink/p/?linkid=9230)">GraphEdit の概要</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSStudio (KsStudio .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\KsStudio.exe</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.exe</p>
<div class="alert">このツールは、管理者特権を持つユーザーが実行する必要
<strong>が   ます</strong>。
</div>
<div>
 
</div></td>
<td align="left"><p>このツールでは、フィルターとフィルターの内部ノードの間のピン留めピン接続を示すフィルターグラフをグラフィカルに表示できます。</p>
<p>%WindowsSdkDir%\tools\x86\KsStudio.chm</p>
<p>%WindowsSdkDir%\tools\x64\KsStudio.chm</p>
<p>詳細については<a href="https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-testing-and-debugging" data-raw-source="[AVStream Testing and Debugging](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-testing-and-debugging)">、「Avstream のテストとデバッグ</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB デバイスビューアー (Usbview .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Usbview.exe</p>
<p>%WindowsSdkDir%\tools\x64\Usbview.exe</p></td>
<td align="left"><p>USB ホストコントローラー、USB ハブ、および接続されている USB デバイスを列挙し、デバイスに関する情報をレジストリから、および USB 要求を介してデバイスに照会できます。</p>
<p>USB デバイスビューアーのソースコードは、コードギャラリーから入手できます。「 <a href="https://go.microsoft.com/fwlink/p/?linkid=256205" data-raw-source="[USBVIEW Sample Application](https://go.microsoft.com/fwlink/p/?linkid=256205)">Usbview サンプルアプリケーション</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

### テクノロジ: Bluetooth ドライバー<a name="tech-bluetooth"></a>

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
<th align="left">説明とヘルプファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Bluetooth 照会レコード検証ツール (Sdpverify .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\Sdpverifiy.exe</p>
<p>%WindowsSdkDir%\tools\x64\Sdpverifiy.exe</p></td>
<td align="left"><p>Windows によって解釈される Bluetooth デバイスの問い合わせレコードを表示します。</p>
<p>WDK のドキュメント:</p>
<p><a href="bluetooth-inquiry-record-verifier.md" data-raw-source="[Bluetooth Inquiry Record Verifier](bluetooth-inquiry-record-verifier.md)">Bluetooth の問い合わせレコードの検証</a></p></td>
</tr>
</tbody>
</table>

 

### テクノロジ: Windows イメージ取得 (WIA) ドライバー<a name="tech_wia"></a>

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
<th align="left">説明とヘルプファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIADbgCfg (Wiadbgcfg)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiadbgcfg.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.exe</p></td>
<td align="left"><p>WIA ドライバーのログ記録を有効にします (Windows Server 2008 以降のバージョンの Windows)。</p>
<div class="alert">
<strong>注</strong>   以前のバージョンの Windows では、WIALogCfg を使用します。
</div>
<div>
 
</div>
<p>%WindowsSdkDir%\tools\x86\wiadbgcfg.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiadbgcfg.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIAInfo2 (Wiainfo2)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x86\wiainfo2.exe</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.exe</p></td>
<td align="left"><p>Wia デバイスドライバーのプロパティを表示および編集できるように、WIA 項目ツリーを表示します。</p>
<p>%WindowsSdkDir%\tools\x86\wiainfo2.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiainfo2.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIAPreview (Wiapreview .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiapreview.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.exe</p></td>
<td align="left"><p>WIA Preview コンポーネントとドライバーのセグメンテーションフィルターを使用する方法について説明します。</p>
<p>%WindowsSdkDir%\tools\x64\wiapreview.htm</p>
<p>%WindowsSdkDir%\tools\x86\wiapreview.htm</p></td>
</tr>
<tr class="even">
<td align="left"><p>WIATest (Wiatest)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wiatest.exe</p>
<p>%WindowsSdkDir%\tools\x86\wiatest.exe</p></td>
<td align="left"><p>ドライバーによって作成された項目ツリー、ドライバーによって公開されている Windows イメージ取得 (WIA) プロパティ、および各プロパティの現在の値が表示されます。 このツールを使用すると、開発および単体テスト中にドライバーをデバッグできます。</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p>
<p>%WindowsSdkDir%\tools\x64\wiatest.htm</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows イメージングトレースファイルビューアー (Wiatrcvw)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\Wiatrcvw.exe</p>
<p>%WindowsSdkDir%\tools\x86\Wiatrcvw.exe</p></td>
<td align="left"><p>WIA トレースログ (%WINDIR%\Debug\WIA\wiatrace.log) を表示し、各モジュールの WIA トレースパラメーターを変更できます。</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p>
<p>%WindowsSdkDir%\tools\x64\Wiatrcvw.mht</p></td>
</tr>
</tbody>
</table>

 

### テクノロジ: Windows ポータブルデバイス (WPD) ドライバー<a name="tech-wpd"></a>

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
<th align="left">説明とヘルプファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WpdDeviceInspector (WpdDeviceInspector)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdDeviceInspector.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdDeviceInspector.exe</p></td>
<td align="left"><p>は、WPD ドライバーに対してクエリを行い、デバイスとその機能を説明する包括的な HTML レポートを生成します。 たとえば、サポートされているデバイスのコマンドとオブジェクトの一覧を取得するために使用できます。 また、このツールでは、各オブジェクトでサポートされているすべてのプロパティの一覧が生成されます。</p>
<p>WDK のドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows ポータブルデバイス</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD ドライバー開発ツール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WpdInfo (WpdInfo .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\WpdInfo.exe</p>
<p>%WindowsSdkDir%\tools\x86\WpdInfo.exe</p></td>
<td align="left"><p>デバイスを開く、閉じる、デバイス上のオブジェクトを作成または削除する、デバイスコマンドを発行するなど、一般的な WPD 操作を実行します。</p>
<p>WDK のドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows ポータブルデバイス</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD ドライバー開発ツール</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft ネットワークモニター (NetMon)</p>
<p><strong>WDK ツール:</strong>違います</p></td>
<td align="left"><p>Microsoft ネットワークモニター (NetMon) をダウンロードし<a href="https://go.microsoft.com/fwlink/p/?linkid=248501" data-raw-source="[here](https://go.microsoft.com/fwlink/p/?linkid=248501)">ます。</a></p></td>
<td align="left"><p>WPD コンポーネントからのトレース情報を表示します。 このツールは、以前のバージョンの WDK に付属していた WpdMon に代わるものです。</p>
<p>WDK のドキュメント:</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=106527" data-raw-source="[Windows Portable Devices](https://go.microsoft.com/fwlink/p/?linkid=106527)">Windows ポータブルデバイス</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262664" data-raw-source="[WPD Driver Development Tools](https://go.microsoft.com/fwlink/p/?linkid=262664)">WPD ドライバー開発ツール</a>、「<a href="https://docs.microsoft.com/previous-versions/hh451296(v=vs.85)" data-raw-source="[Using the Network Monitor Tool](https://docs.microsoft.com/previous-versions/hh451296(v=vs.85))">ネットワークモニターツールの使用</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

### テクノロジ: プリンタードライバー<a name="tech-printer"></a>

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
<th align="left">説明とヘルプファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GPDCheck (gpdcheck)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\gpdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\gpdcheck.exe</p></td>
<td align="left"><p>一般的なプリンター記述ファイル (GPD) の構文の正確性を検証します。</p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>gpdcheck/?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>INFGate (Infgate)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\infgate.exe</p>
<p>%WindowsSdkDir%\tools\x86\infgate.exe.exe</p></td>
<td align="left"><p>プリンターの INF ファイルに準拠しているかどうかを検証します。</p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>infgate/?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>isXPS (isXPS .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\isxps\isxps.exe</p>
<p>%WindowsSdkDir%\tools\x86\isxps\isxps.exe</p></td>
<td align="left"><p>Xps ファイルが XPS および OPC 仕様に準拠しているかどうかを検証します。</p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>isxps/?</strong> コマンドプロンプトウィンドウに表示されます。</p>
<p>詳細については、「 <a href="https://go.microsoft.com/fwlink/p/?linkid=150004" data-raw-source="[isXPS Conformance Tool](https://go.microsoft.com/fwlink/p/?linkid=150004)">Isxps 適合性ツール</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ルック sgood (Look Sgood .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\looksgood.exe</p>
<p>%WindowsSdkDir%\tools\x86\looksgood.exe</p></td>
<td align="left"><p>XPS レンダリングエンジンの正確性を検証します。</p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>いいですか?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeNTF (Makentf)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\makentf.exe</p>
<p>%WindowsSdkDir%\tools\x86\makentf.exe</p></td>
<td align="left"><p>Adobe Font Metrics (AFM) ファイルと東アジア言語のフォント AFM ファイルを Windows フォントファイル (ntf) に変換します。</p>
<p>WDK のドキュメント:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/print/converting-afm-files-to-ntf-files" data-raw-source="[Converting AFM Files to NTF Files](https://docs.microsoft.com/windows-hardware/drivers/print/converting-afm-files-to-ntf-files)">AFM ファイルから NTF ファイルへの変換</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/print/converting-east-asian-afm-files-to-ntf-files" data-raw-source="[Converting East Asian AFM Files to NTF Files](https://docs.microsoft.com/windows-hardware/drivers/print/converting-east-asian-afm-files-to-ntf-files)">東アジアの AFM ファイルから NTF ファイルへの変換</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PPDCheck (Ppdcheck .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ppdcheck.exe</p>
<p>%WindowsSdkDir%\tools\x86\ppdcheck.exe</p></td>
<td align="left"><p>PostScript プリンター記述ファイル (PPD) の構文の正確性を検証します。</p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>ppdcheck/?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PTConform (PTConform .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PTConform.exe</p>
<p>%WindowsSdkDir%\tools\x86\PTConform.exe</p></td>
<td align="left"><p>印刷チケットまたは印刷機能のドキュメントが印刷スキーマに準拠しているかどうかを検証します。</p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>ptconform/?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>XpsAnalyzer (XpsAnalyzer)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\XpsAnalyzer.exe</p>
<p>%WindowsSdkDir%\tools\x86\XpsAnalyzer.exe</p></td>
<td align="left"><p>XPS 1.0 仕様との互換性のために、XML Paper Specification (XPS) ファイルを分析します。</p>
<p>WDK のドキュメント:</p>
<p><a href="xpsanalyzer.md" data-raw-source="[XpsAnalyzer](xpsanalyzer.md)">XpsAnalyzer</a></p></td>
</tr>
</tbody>
</table>

 

### テクノロジ: センサー<a name="tech-sensors"></a>

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
<th align="left">説明とヘルプファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>センサー診断ツール (sensordiagnostictool)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>センサーと場所の機能について、ドライバー、ファームウェア、およびハードウェアをテストします。 このツールでは、センサーと場所 API を呼び出して、データの取得、イベント処理、レポート間隔、変更の感度、プロパティの取得をテストします。</p>
<p>WDK のドキュメント:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/sensors/the-sensor-diagnostic-tool" data-raw-source="[Testing sensor functionality with the Sensor Diagnostic Tool](https://docs.microsoft.com/windows-hardware/drivers/sensors/the-sensor-diagnostic-tool)">センサー診断ツールを使用したセンサー機能のテスト</a></p></td>
</tr>
</tbody>
</table>

 

### テクノロジ: すべてのドライバー<a name="tech-all"></a>

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
<th align="left">説明とヘルプファイルの場所</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ビンの位置 (ビンプレース .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\binplace.exe</p></td>
<td align="left"><p>ファイルの移動、実行可能ファイルからのシンボルの抽出、およびシンボルファイルからのプライベートシンボルの削除によって、大規模なコードプロジェクトを管理します。</p>
<p>WDK のドキュメント:</p>
<p><a href="binplace.md" data-raw-source="[BinPlace](binplace.md)">ビンの位置</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバーのコード分析</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>コード分析ツールは Visual Studio に含まれています。 ドライバー固有のコンポーネントは、WDK をインストールするときに追加されます。</p></td>
<td align="left"><p>C およびC++コードエラーを検出する静的な検証ツール。 このバージョンは、カーネルモードドライバーのエラーを検出するように特別に設計されています。</p>
<div class="alert">
<strong>注</strong>  以前のバージョンの WDK では、この機能は oacr に含まれており、スタンドアロンツールのドライバー用 PREfast としても使用できました。 Visual Studio 2012 以降、この機能は Visual Studio に統合されました。
</div>
<div>
 
</div>
<p>WDK のドキュメント:</p>
<p><a href="code-analysis-for-drivers.md" data-raw-source="[Code Analysis for Drivers](code-analysis-for-drivers.md)">ドライバーのコード分析</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Certmgr.exe (Certmgr.exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\CertMgr.exe</p>
<p>%WindowsSdkDir%\bin\x86\CertMgr.exe</p></td>
<td align="left"><p>ドライバーと<a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver packages](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">ドライバーパッケージ</a>の署名に使用される証明書、証明書信頼リスト (ctl)、および証明書失効リスト (crl) を管理します。</p>
<p>WDK のドキュメント:</p>
<p><a href="certmgr.md" data-raw-source="[&lt;strong&gt;CertMgr&lt;/strong&gt;](certmgr.md)"><strong>Certmgr.exe</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ChkINF</p>
<p><strong>WDK ツール:</strong>れ</p></td>
<td align="left"><p>前のパス:</p>
<p>%WindowsSdkDir%\tools\x86\Chkinf</p></td>
<td align="left"><p>ChkInf は非推奨となりました。 代わりに、 <a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a>を使用してください。</p>
<p>WDK のドキュメント:</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>コンピューターのハードウェア識別ツール (Computerhardware Ids .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p><strong>Windows Driver Kit (WDK) 8:</strong></p>
<p>%WindowsSdkDir%\tools\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\tools\x86\ComputerHardwareIds.exe</p>
<p>WDKPath\tools\Other\ia64\ComputerHardwareIds.exe</p>
<p><strong>Windows Driver Kit (WDK) 8.1:</strong></p>
<p>%WindowsSdkDir%\bin\x64\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\x86\ComputerHardwareIds.exe</p>
<p>%WindowsSdkDir%\bin\arm\ComputerHardwareIds.exe</p></td>
<td align="left"><p>コンピューターのハードウェア Id を SMBIOS 情報から派生します。</p>
<p>WDK のドキュメント:</p>
<p><a href="computerhardwareids.md" data-raw-source="[ComputerHardwareIds](computerhardwareids.md)">コンピューターのハードウェア Id</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>DC2WMIParser (DC2WMIParser)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\DC2WMIParser.exe</p>
<p>%WindowsSdkDir%\tools\x86\DC2WMIParser.exe</p></td>
<td align="left"><p>DC2WMIParser は、ドライバーの検証ツールによって作成された WMI IRP レコードを収集し、このログをテキストファイルに変換するツールです。</p>
<p>書</p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=698758" data-raw-source="[IRP Logging](https://go.microsoft.com/fwlink/p/?LinkId=698758)">IRP ログ</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>依存関係のウォーカー (.exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\depends.exe</p>
<p>%WindowsSdkDir%\tools\x86\depends.exe</p></td>
<td align="left"><p>アプリケーションで必要とされるモジュールの依存パターンをツリーダイアグラムで表示します。 表示には、各モジュールによってエクスポートされた関数、他のモジュールによって実際に呼び出される関数、およびモジュールを読み込んで実行するために必要な最小ファイルセットなど、多くの詳細が含まれます。</p>
<p>ツールで、<strong>依存関係のウォーカー</strong>のヘルプメニューから [<strong>ヘルプトピック</strong>] を選択します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DevCon (Devcon)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\devcon.exe</p>
<p>%WindowsSdkDir%\tools\x86\devcon.exe</p></td>
<td align="left"><p>デバイスマネージャーのコマンドラインバージョン。 DevCon ローカルコンピューター上のデバイスを有効、無効、インストール、構成、および削除し、ローカルコンピューターとリモートコンピューター上のデバイスに関する詳細情報を表示します。</p>
<p>WDK のドキュメント:</p>
<p><a href="devcon.md" data-raw-source="[DevCon](devcon.md)">DevCon</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ドライバー (Drivers)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\drivers.exe</p>
<p>%WindowsSdkDir%\tools\x86\drivers.exe</p></td>
<td align="left"><p>コンピューターにインストールされているすべてのドライバーの一覧を表示します。</p>
<p>WDK のドキュメント:</p>
<p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバーの検証ツール (Verifier)</p>
<p><strong>WDK ツール:</strong>違います</p></td>
<td align="left"><p>%Windir%\system32\verifier.exe</p></td>
<td align="left"><p>カーネルモードドライバーとグラフィックスドライバーを監視して、無効な関数呼び出しまたはシステムを破損する可能性があるアクションを検出します。 ドライバーがさまざまなストレスを受け、不適切な動作を検出するテストを行うことができます。</p>
<p>WDK のドキュメント:</p>
<p><a href="driver-verifier.md" data-raw-source="[Driver Verifier](driver-verifier.md)">ドライバー検証ツール</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ドライバー検証ログ (DVL)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>Microsoft Visual Studio と WDK が必要です。 [<strong>ドライバー</strong> ] メニューの [<strong>ドライバー検証ログの作成</strong>...] をクリックします。</p></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=227016" data-raw-source="[Windows Server 2012 Hardware Certification Program](https://go.microsoft.com/fwlink/p/?linkid=227016)">Windows Server 2012 ハードウェア認定プログラム</a>では、該当するすべてのドライバー送信にドライバー検証ログ (dvl) が必要です。 DVL には、コード分析と静的ドライバー検証ツールのログ ファイルからの結果の要約が含まれています。 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Creating a Driver Verification Log](https://docs.microsoft.com/windows-hardware/drivers)">ドライバー検証ログの作成」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>拡張ストレージ証明書管理ツール (EhStorCertMgrCmd)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\ehstorcertmgrcmd.exe</p>
<p>%WindowsSdkDir%\tools\x86\ehstorcertmgrcmd.exe</p></td>
<td align="left"><p>IEEE 1667 標準に準拠している USB 記憶装置の証明書を管理します。</p>
<p>WDK のドキュメント:</p>
<p><a href="enhanced-storage-certificate-management-tool.md" data-raw-source="[Enhanced Storage Certificate Management Tool](enhanced-storage-certificate-management-tool.md)">拡張ストレージ証明書管理ツール</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>イベントおよびパフォーマンスカウンターマニフェストジェネレーターツール (ECManGen)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\ECManGen.exe</p>
<p>%WindowsSdkDir%\bin\x86\ECManGen.exe</p></td>
<td align="left"><p>XML タグを使用しなくても、イベントまたはパフォーマンスカウンターマニフェスト (* 男性) をゼロから作成するためのツール。 マニフェストファイルの作成の詳細については、「<a href="https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest" data-raw-source="[Writing an Instrumentation Manifest (Windows)](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)">インストルメンテーションマニフェスト (Windows) の記述</a>」と「<a href="adding-event-tracing-to-kernel-mode-drivers.md" data-raw-source="[Adding Event Tracing to Kernel-Mode Drivers](adding-event-tracing-to-kernel-mode-drivers.md)">カーネルモードドライバーへのイベントトレースの追加</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Guidgen.exe (Guidgen.exe)</p>
<p><strong>WDK ツール:</strong>違います</p></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=121586" data-raw-source="[Microsoft Exchange Server GUID Generator](https://go.microsoft.com/fwlink/p/?linkid=121586)">Microsoft Exchange SERVER GUID ジェネレーター</a>からダウンロード可能</p></td>
<td align="left"><p>クラス、オブジェクト、およびインターフェイスを識別するために使用できるグローバル一意識別子 (GUID) を生成します。 生成された GUID は、ソースコードに挿入できるように、4つの形式のいずれかでクリップボードにコピーされます。</p>
<p>GUIDGEN.EXE (ダウンロードパッケージに含まれています)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Inf2Cat (Inf2cat)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\inf2cat.exe</p>
<p>%WindowsSdkDir%\bin\x86\inf2cat.exe</p></td>
<td align="left"><p>指定された Windows バージョンの一覧に対して<a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver package's](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">ドライバーパッケージの</a>INF ファイルにデジタル署名できるかどうかを判断し、指定した場合は、指定した windows バージョンに適用される署名されていない<a href="https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files" data-raw-source="[catalog files](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)">カタログファイル</a>を生成します。</p>
<p>WDK のドキュメント:</p>
<p><a href="inf2cat.md" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](inf2cat.md)"><strong>Inf2Cat</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>InfVerif (InfVerif)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>c:\Program Files(x86)\Windows Kits\10\tools\arm\infverif.exe</p>
<p>c:\Program Files(x86)\Windows Kits\10\tools\arm64\infverif.exe</p>
<p>c:\Program Files (x86) \Windows Kits\10\tools\x86\infverif.exe</p>
<p>c:\Program Files (x86) \Windows Kits\10\tools\x64\infverif.exe</p>
<td align="left"><p>ドライバーの INF ファイルをテストします。 Inf 構文の問題を報告するだけでなく、INF ファイルがユニバーサルであるかどうかが報告されます。</p>
<p>WDK のドキュメント:</p>
<p><a href="infverif.md" data-raw-source="[InfVerif](infverif.md)">InfVerif</a></p></td>
</tr>

<tr class="even">
<td align="left"><p>MakeCat (MakeCat)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>WDKPath\bin\amd64\MakeCat.exe</p>
<p>WDKPath\bin\ia64\MakeCat.exe</p>
<p>WDKPath\bin\x86\MakeCat.exe</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver package](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">ドライバーパッケージ</a>の<a href="https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files" data-raw-source="[catalog file](https://docs.microsoft.com/windows-hardware/drivers/install/catalog-files)">カタログファイル</a>を作成します。</p>
<p>WDK のドキュメント:</p>
<p><a href="makecat.md" data-raw-source="[MakeCat](makecat.md)">MakeCat</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>MakeCert (MakeCert)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\MakeCert.exe</p>
<p>%WindowsSdkDir%\bin\x86\MakeCert.exe</p></td>
<td align="left"><p>システムテストルートキーまたは指定した別のキーによって署名された x.509 証明書を作成します。</p>
<p>WDK のドキュメント:</p>
<p><a href="makecert.md" data-raw-source="[&lt;strong&gt;MakeCert&lt;/strong&gt;](makecert.md)"><strong>MakeCert</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>MSBuild (Msbuild.exe)</p>
<p><strong>WDK ツール:</strong>違います</p></td>
<td align="left"><p>Visual Studio と共にインストールされます。</p></td>
<td align="left"><p>Microsoft WDK で提供されるサンプル、ドライバー、および関連するソフトウェアコンポーネントを構築します。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=262804" data-raw-source="[MSBuild]( https://go.microsoft.com/fwlink/p/?linkid=262804)">MSBuild</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PnpCpu (PnPCpu)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\PnPCpu.exe</p>
<p>%WindowsSdkDir%\tools\x86\PnPCpu.exe</p></td>
<td align="left"><p>Windows Server 2008 の実行中のインスタンスへのプロセッサのホットアドをシミュレートします。</p>
<p>WDK のドキュメント:</p>
<p><a href="pnpcpu.md" data-raw-source="[PNPCPU](pnpcpu.md)">PNPCPU</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PnPUtil (PnPUtil)</p>
<p><strong>WDK ツール:</strong>違います</p></td>
<td align="left"><p>%Windir%\system32\pnputil.exe</p></td>
<td align="left"><p>Windows ドライバーストアから<a href="https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages" data-raw-source="[driver packages](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)">ドライバーパッケージ</a>をインストールまたは削除するコマンドラインツール。</p>
<p>このツールは、windows 7 以降のバージョンの Windows で使用できます。</p>
<p>WDK のドキュメント:</p>
<p><a href="pnputil.md" data-raw-source="[PnPUtil](pnputil.md)">PnPUtil</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>PoolMon (Poolmon)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\poolmon.exe</p>
<p>%WindowsSdkDir%\tools\x86\poolmon.exe</p></td>
<td align="left"><p>システムのページングされたカーネルプールと、ターミナルサービスセッションに使用されるメモリプールから、オペレーティングシステムがメモリの割り当てについて収集したデータを表示します。 データはプール割り当てタグによってグループ化されます。</p>
<p>WDK のドキュメント:</p>
<p><a href="poolmon.md" data-raw-source="[PoolMon](poolmon.md)">PoolMon</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PowerCfg (PowerCfg)</p>
<p><strong>WDK ツール:</strong>違います</p></td>
<td align="left"><p>%Windir%\system32\powercfg.exe</p></td>
<td align="left"><p>システムのエネルギー効率を評価するために使用されるコマンドラインツールです。</p>
<p>このツールは、windows 7 以降のバージョンの Windows で使用できます。</p>
<p>デベロッパーセンターのドキュメント:</p>
<a href="https://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx" data-raw-source="[Using PowerCfg to Evaluate System Energy Efficiency](https://download.microsoft.com/download/7/E/7/7E7662CF-CBEA-470B-A97E-CE7CE0D98DC2/PowerCfg.docx)">PowerCfg を使用したシステムエネルギー効率の評価</a>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p></p>
<p><strong>PowerCfg/?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Pvk2Pfx (Pvk2Pfx)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\Pvk2Pfx.exe</p>
<p>%WindowsSdkDir%\bin\x86\Pvk2Pfx.exe</p></td>
<td align="left"><p>.Spc、.cer、および .pvk ファイルに格納されている公開キーと秘密キーの情報を personal information exchange (.pfx) ファイルにコピーします。</p>
<p>WDK のドキュメント:</p>
<p><a href="pvk2pfx.md" data-raw-source="[&lt;strong&gt;Pvk2Pfx&lt;/strong&gt;](pvk2pfx.md)"><strong>Pvk2Pfx</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>PwrTest (Pwrtest .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\pwrtest.exe</p>
<p>%WindowsSdkDir%\tools\x86\pwrtest.exe</p></td>
<td align="left"><p>コンピューターから電源管理情報を記録して記録する Windows 7 以降用の電源管理ツール。</p>
<p>WDK のドキュメント:</p>
<p><a href="pwrtest.md" data-raw-source="[PwrTest](pwrtest.md)">PwrTest</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>SignTool (SignTool)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\SignTool.exe</p>
<p>%WindowsSdkDir%\bin\x86\SignTool.exe</p></td>
<td align="left"><p>ファイルにデジタル署名し、ファイルの署名を検証し、ファイルにタイムスタンプを付ける。</p>
<p>WDK のドキュメント:</p>
<p><a href="signtool.md" data-raw-source="[&lt;strong&gt;SignTool&lt;/strong&gt;](signtool.md)"><strong>SignTool</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Stampinf (Stampinf)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\stampinf.exe</p>
<p>%WindowsSdkDir%\bin\x86\stampinf.exe</p></td>
<td align="left"><p><strong>DriverVer</strong>ディレクティブなど、一般的な INF ファイルディレクティブを更新します。</p>
<p>WDK のドキュメント:</p>
<p><a href="stampinf.md" data-raw-source="[Stampinf](stampinf.md)">Stampinf</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>静的ドライバー検証ツール</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\SDV</p>
<p></p>
<div class="alert">Visual Studio の [<strong>ドライバー</strong> ] メニューから [Static driver Verifier] を
<strong>起動  ます</strong>。
</div>
<div>
 
</div></td>
<td align="left"><p>Windows ドライバーのソースコードを体系的に分析し、ドライバーが Windows オペレーティングシステムのカーネルと適切に対話するかどうかを判断するドライバー用の静的検証ツール。</p>
<p>WDK のドキュメント:</p>
<p><a href="static-driver-verifier.md" data-raw-source="[Static Driver Verifier](static-driver-verifier.md)">静的ドライバー検証ツール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Tracefmt (Tracefmt .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracefmt.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracefmt.exe</p></td>
<td align="left"><p>イベントトレースログファイル (.etl) またはリアルタイムトレースセッションからのトレースメッセージを書式設定して表示します。</p>
<p>WDK のドキュメント:</p>
<p><a href="tracefmt.md" data-raw-source="[Tracefmt](tracefmt.md)">Tracefmt</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>TraceLog (Tracelog .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p><strong>WDK 8:</strong></p>
<p>%WindowsSdkDir%\tools\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\tools\x86\tracelog.exe</p>
<p><strong>WDK 8.1:</strong></p>
<p>%WindowsSdkDir%\bin\x64\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracelog.exe</p>
<p>%WindowsSdkDir%\bin\arm\tracelog.exe</p></td>
<td align="left"><p>コマンドラインからトレースセッションを構成し、制御します。 遅延プロシージャ呼び出し (Dpc) と割り込みサービスルーチン (Isr) で費やされた時間を計測します。</p>
<p>WDK のドキュメント:</p>
<p><a href="tracelog.md" data-raw-source="[Tracelog](tracelog.md)">トレースログ</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TracePDB (Tracepdb .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracepdb.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracepdb.exe</p></td>
<td align="left"><p>WPP トレースプロバイダーの完全またはプライベートの PDB シンボルファイルから、トレースメッセージ形式 (tmf) ファイルを作成します。</p>
<p>WDK のドキュメント:</p>
<p><a href="tracepdb.md" data-raw-source="[Tracepdb](tracepdb.md)">Tracepdb</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>TraceView (Traceview .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\TraceView.exe</p>
<p>%WindowsSdkDir%\tools\x86\TraceView.exe</p></td>
<td align="left"><p>トレースセッションを構成および制御し、リアルタイムのトレースセッションとトレースログからの書式付きトレースメッセージを表示します。 TraceView には、バッチ処理とスクリプト作成用のグラフィックユーザーインターフェイスとコマンドラインインターフェイスがあります。</p>
<p>WDK のドキュメント:</p>
<p><a href="traceview.md" data-raw-source="[TraceView](traceview.md)">TraceView</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>TraceWPP (Tracewpp)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\tracewpp.exe</p>
<p>%WindowsSdkDir%\bin\x86\tracewpp.exe</p></td>
<td align="left"><p>Windows Software Trace プリプロセッサ (WPP) を実行します。</p>
<p>WDK のドキュメント:</p>
<p><a href="wpp-preprocessor.md" data-raw-source="[WPP Preprocessor](wpp-preprocessor.md)">WPP プリプロセッサ</a></p>
<p><a href="survey-of-software-tracing-tools.md" data-raw-source="[Survey of Software Tracing Tools](survey-of-software-tracing-tools.md)">ソフトウェアトレースツールの調査</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WDF Tester</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64&lt;/p&gt;
<p>%WindowsSdkDir%\tools\x86&lt;/p&gt;</td>
<td align="left"><p>WDF ドライバーをテスト、検証、およびデバッグするために使用できる一連のツール。 ツールセットには、スクリプトまたはコンパイル済みアプリケーションで使用できる WMI プログラミングインターフェイスが用意されています。</p>
<p>WDK のドキュメント:</p>
<p><a href="wdftester--wdf-driver-testing-toolset.md" data-raw-source="[WdfTester: WDF Driver Testing Toolset](wdftester--wdf-driver-testing-toolset.md)">WdfTester: WDF Driver テストツールセット</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WDF Verifier (Wdfverifier .exe)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\wdfverifier.exe</p>
<p>%WindowsSdkDir%\tools\x86\wdfverifier.exe</p></td>
<td align="left"><p>KMDF および UMDF ドライバーのフレームワークの検証機能に使いやすいインターフェイスを提供します。</p>
<p>WDK のドキュメント:</p>
<p><a href="wdf-verifier-control-application.md" data-raw-source="[WDF Verifier Control Application](wdf-verifier-control-application.md)">WDF 検証コントロールアプリケーション</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Web Services on devices (WSD) 基本的な相互運用性ツール (WSDBIT)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p><strong>WSDBIT クライアント:</strong></p>
<p>%WindowsSdkDir%\tools\x64\ wsdbit_client</p>
<p>%WindowsSdkDir%\tools\x86\ wsdbit_client</p>
<p><strong>WSDBIT サーバー:</strong></p>
<p>%WindowsSdkDir%\tools\x64\ wsdbit_server</p>
<p>%WindowsSdkDir%\tools\x86\ wsdbit_server</p></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=81255" data-raw-source="[Device Profile for Web Services (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)">Web サービス (DPWS) のデバイスプロファイル</a>の実装が、WSDAPI で動作することを確認します。</p>
<p>WDK のドキュメント:</p>
<p><a href="wsdapi-basic-interoperability-tool.md" data-raw-source="[WSD Interoperability Tool](wsdapi-basic-interoperability-tool.md)">WSD 相互運用性ツール</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Winerror.h (Winerror.h)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\tools\x64\winerror.exe</p>
<p>%WindowsSdkDir%\tools\x86\winerror.exe</p></td>
<td align="left"><p>指定されたエラー (Winerror.h) または成功コード (Ntstatus) のエラーメッセージ識別子およびマッピング情報を返します。</p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>winerror.h/?</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WMIMofCk (Wmimofck)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x86\wmimofck.exe</p></td>
<td align="left"><p>WDK のドキュメント:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe" data-raw-source="[Using wmimofck.exe](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe)">Wmimofck の使用</a></p>
<p>コマンドオプションの詳細については、「」と入力してください。</p>
<p><strong>wmimofck -?</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>WsdCodeGen (Wsdcodegen)</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p>%WindowsSdkDir%\bin\x64\wsdcodegen.exe</p>
<p>%WindowsSdkDir%\bin\x86\wsdcodegen.exe</p></td>
<td align="left"><p>Web サービスコントラクトに基づいてプロキシとスタブを自動的に生成します。 主に、このツールを使用してクライアントアプリケーションを作成できます。 ただし、テストに使用したり、ユーザーモードドライバーを作成したりすることはできます。</p>
<p>バイナリ MOF ファイル (bmf) で指定されたクラス、プロパティ、メソッド、およびイベントが WMI での使用に対して有効であることを確認します。 MOF サポートファイルを生成します。</p>
<p>Windows SDK：</p>
<p>「<a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">デバイスの Web サービス</a>」セクションを参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WSDDebug_client と WSDDebug_host</p>
<p><strong>WDK ツール:</strong>うん</p></td>
<td align="left"><p><strong>デバッグクライアント:</strong></p>
<p>%WindowsSdkDir%\bin\x64\ WSDDebug_client</p>
<p>%WindowsSdkDir%\bin\x86\ WSDDebug_client</p>
<p><strong>デバッグホスト:</strong></p>
<p>%WindowsSdkDir%\bin\x64\ WSDDebug_host</p>
<p>%WindowsSdkDir%\bin\x86\ WSDDebug_host</p></td>
<td align="left"><p>これらのツールは、デバイスまたはアプリケーションのトラブルシューティングに使用できるソフトデバイスとクライアントです。</p>
<p>Windows SDK：</p>
<p>「<a href="https://go.microsoft.com/fwlink/p/?linkid=81407" data-raw-source="[Web Services on Devices](https://go.microsoft.com/fwlink/p/?linkid=81407)">デバイスの Web サービス</a>」セクションを参照してください。</p></td>
</tr>
</tbody>
</table>

 

### WDK for Windows 8.1 の新機能<a name="what-s-new-in-the-wdk-for-windows8-1"></a>

WDK 8.1 では、次のツールが追加または変更されています。

-   HCK テストスイート (「 [Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)」および「 [WDK 8.1 で hck テストスイートを実行する方法](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください)。

-   [Driver Verifier](driver-verifier.md): Windows ドライバーのエラーを検出するための4つの新しいオプションが追加されました。
-   [Pwrtest](pwrtest.md): 更新されたドキュメント、新しいテストシナリオ (コネクトスタンバイ電源状態のサポートなど)。
-   [Tracelog](tracelog.md)-新しいオプション。

### Windows 8 用 WDK の新機能<a name="what-s-new-in-the-wdk-for-windows8"></a>

Windows 8 用の WDK には、次のツールが追加されています。

-   Bluetooth 照会レコード検証ツール (Sdpverify .exe)

-   デバイスの基本テスト (「 [Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)」および「[デバイスの基本テストを選択して構成する方法](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください)。

-   センサー診断ツール (sensordiagnostictool)

### Windows 8 用 WDK の変更点<a name="what-s-changed-in-the-wdk-for-windows8"></a>
次のツールは、Microsoft WDK for Windows 7 に含まれていましたが、Windows 8 用 WDK には含まれていません。

-   Windows 生体認証フレームワークツール (BioTest、WBDIDriverTest)

-   デバイスパス Exerciser (devpathexer .exe)。 現在、デバイスの基本的なファジーテストの一部です。

-   IoSpy と Iospy (IoSpyCmd、Iospy .exe)。 現在、デバイスの基本的なテストの一部です。

-   Kernrate (Kernrate .exe) Kernrate はサポートされなくなりました。 代わりに、 [Windows Performance Analysis Toolkit](https://go.microsoft.com/fwlink/p/?linkid=294280)を使用してください。

-   Microsoft 自動コードレビュー (OACR) (ドライバーコンポーネントが Visual Studio のコード分析ツールの一部になりました)

-   プラグアンドプレイドライバーテスト (pnpdtest .exe)。 現在、デバイスの基本的なテストの一部です。

-   ProCalc

-   WWAN ドライバーテストアプリ (wwandrivertestapp .exe)

### <a name="supported-platforms"></a>サポートされているプラットフォーム

WDK 8.1 は、次のバージョンの Windows で実行されるドライバーの開発をサポートしています。

-   Windows 8.1 と Windows 8

-   Windows Server 2012 R2 および Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

-   Windows Vista (SP1 と SP2 を含む) の場合は、WDK 8 を使用する必要があります。 Windows XP の場合は、WDK 7 を使用する必要があります。

これらのバージョンの Windows では、統合された Visual Studio ドライバー開発環境を実行できます。

-   Windows 8.1 と Windows 8

-   Windows Server 2012 R2 および Windows Server 2012

-   Windows 7

-   Windows Server 2008 R2

 

 


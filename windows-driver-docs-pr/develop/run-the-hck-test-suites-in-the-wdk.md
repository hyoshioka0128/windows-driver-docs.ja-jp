---
ms.assetid: 3FC63BAD-4B95-40AB-BFBE-88A3274B76E8
title: WDK 8.1 の HCK テスト スイートを実行する方法
description: WDK で Windows ドライバーをより簡単にテストできるようにするために、WDK 8.1 以降では、テスト コンピューターで実行する HCK テスト スイートを選べるようになりました。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186461bfda62753dd3e9e5998e8dd257d476df1e
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "70020668"
---
# <a name="how-to-run-the-hck-test-suites-in-wdk-81"></a>WDK 8.1 の HCK テスト スイートを実行する方法

WDK で Windows ドライバーをより簡単にテストできるようにするために、WDK 8.1 以降では、テスト コンピューターで実行する HCK テスト スイートを選べるようになりました。 [HCK テスト スイート](#HCK_test_suites)には、デバイスの基本機能のテストや、グラフィックス、イメージング、ワイヤレス LAN、モバイル ブロードバンド (CDMA と GSM)、WiFi Direct デバイスのテストが含まれています。 これらのテストは、Windows ハードウェア認定キット (Windows HCK) で使われているテストと同じです。 Windows HCK について詳しくは、[Windows ハードウェア認定プログラムに関するページ](https://go.microsoft.com/fwlink/p/?linkid=8705)をご覧ください。

HCK テストは、コマンド プロンプト ウィンドウまたは Visual Studio から実行できます。 また、これらのテストを新しい場所 (別のコンピューターや USB キー ドライブなど) にコピーして、その場所からテストを実行することもできます。 テストを起動すると、テストの実行に必要なローカル構成が自動的に設定されます。

-   [Visual Studio を使ったテスト コンピューターでの HCK テスト スイートの実行](#run_hck_from_vs)
-   [コマンド プロンプト ウィンドウからの HCK テスト スイートの実行](#run_hck_script)

## <a name="span-idrun_hck_from_vsspanspan-idrun_hck_from_vsspanrunning-the-hck-test-suites-on-a-test-computer-using-visual-studio"></a><span id="run_hck_from_vs"></span><span id="RUN_HCK_FROM_VS"></span>Visual Studio を使ったテスト コンピューターでの HCK テスト スイートの実行


まだ準備ができていない場合は、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の指示に従ってください。 テスト コンピューターの構成が終わったら、テスト コンピューターの名前がツール バーに表示されます。 HCK テスト スイートでテストするデバイス用に構成したテスト コンピューターを選んでいることを確認します。

デバイスとドライバー、およびテスト トポロジの追加要件がある場合 (テストするデバイスの HCK テスト前提条件を参照) はそれらをインストールして、必要に応じてテスト コンピューターを準備します。 HCK Studio と HCK コントローラーの代わりに、Visual Studio と WDK 8.1 を使ってテストを実行できます。

**テスト コンピューターで実行する HCK テスト スイートの選ぶには**

1.  **[ドライバー]** メニューで、 **[テスト]** 、 **[Test Group Explorer] (テスト グループ エクスプローラー)** の順にクリックします。
2.  **[Driver Test Group Explorer] (ドライバー テスト グループ エクスプローラー)** ウィンドウで、いずれかの [HCK テスト スイート](#HCK_test_suites)をクリックします。

    テスト スイートを選ぶと、そのテスト スイートが **[Driver Test Group] (ドライバー テスト グループ)** ウィンドウに表示されます。

3.  HCK テスト スイートでテストするデバイス用に構成したテスト コンピューターを選んでいることを確認します。
4.  HCK テスト スイートを使うには、テストするデバイスの構成要件も満たす必要があります。
5.  チェック ボックスを使って、目的とするテスト コンピューターのアーキテクチャ (x86、x64、ARM) に対応したテストを選ぶことができます。
6.  **[ドライバー]** メニューで、 **[テスト] &gt; [テストの実行]** の順にクリックします。 [テストの実行] は既定で、現在選択されているテスト グループのすべてのテストを実行します。

用意された HCK テスト スイートのいずれかをコピーし、必要なテスト サポート ファイルと共にエクスポートすることにより、コマンド プロンプト ウィンドウからテスト スイートを実行することもできます。

**テスト スイートをエクスポートするには**

1.  **[Test Group Explorer (テスト グループ エクスプローラー)]** で、コピーする HCK テスト スイートを右クリックし、ショートカット メニューから **[Export Test Suite... (テスト スイートのエクスポート...)]** をクリックします (コマンドにより **CopyMe.cmd** スクリプトが実行されます)。
2.  テスト スイートのコピー先フォルダーを選択します。 テスト スイートは、ネットワーク共有または USB フラッシュ ドライブにエクスポートできます。
3.  HCK テスト スイートを実行するには、テスト コンピューターで管理者特権のアクセス許可を使ってコマンド プロンプト ウィンドウを開きます。 コピー先ディレクトリに移動して **RunMe.cmd** スクリプトを実行します。 詳しくは、「[コマンド プロンプト ウィンドウから HCK テスト スイートを実行するには](#RunMe)」を参照してください。

## <a name="span-idrun_hck_scriptspanspan-idrun_hck_scriptspanrunning-the-hck-test-suites-from-a-command-prompt-window"></a><span id="run_hck_script"></span><span id="RUN_HCK_SCRIPT"></span>コマンド プロンプト ウィンドウからの HCK テスト スイートの実行


**HCK テスト スイートのコピー**

1.  Visual Studio のコマンド プロンプト ウィンドウを開きます。 %WindowsSdkDir%\\Testing\\Tests\\HCK Tests\\Basic ディレクトリに移動します (例: C:\\Program Files (x86)\\Windows Kits\\8.1\\Testing\\Tests\\HCK Tests\\Basic)
2.  **CopyMe.cmd** スクリプトを実行し、テスト スイートの名前とコピー先ディレクトリを指定します。 スクリプトの構文は次のとおりです。

    ```cpp
    CopyMe.cmd testSuite destinationPath
    ```

    *testSuite* は次のいずれかです。

    -   Device.Device Fundamentals

    -   Device.Graphics

    -   Device.Imaging

    -   Device.Network.MobileBroadband.CDMA

    -   Device.Network.MobileBroadband.GSM

    -   Device.Network.WLAN

    *destinationPath* では、UNC パスを含む任意の有効なパスを指定できます。 たとえば、HCK テスト スイート USB フラッシュ ドライブやサーバー上の共有にコピーできます。

    ```cpp
    C:\Program Files (x86)\Windows Kits\8.1\Testing\Tests\HCK Tests\Basic>CopyMe "De
    vice.Device Fundamentals" d:\temp\devfund
    Copying test target setup installers
    Copying TAEF and WDTF infrastructure
    Copying debuggers infrastructure
    Copying x86 tools
    Copying x64 tools
    Copying arm tools
    Copying test suite
    Copy complete!

    Run on any computer using an administrator command prompt in the same folder as
    the RunMe.cmd script.
    "RunMe.cmd <infFileName>"
    ```

<span id="RunMe"></span><span id="runme"></span><span id="RUNME"></span>
**注**  テスト コンピューターで Windows 7 を実行している場合、HCK テスト スイートを実行する前に [Microsoft .NET Framework 4.5](https://go.microsoft.com/fwlink/p/?linkid=317996) をダウンロードしてインストールする必要があります。

 

**コマンド プロンプト ウィンドウからの HCK テスト スイートを実行するには**

1.  テスト用に構成したテスト コンピューターで、管理者特権のアクセス許可を使って ( **[管理者として実行]** ) コマンド プロンプト ウィンドウを開き、HCK テスト スイートをコピーしたディレクトリに移動します。

2.  **RunMe.cmd** スクリプトを実行し、INF ファイルのパスと名前を指定します。 スクリプトの構文は次のとおりです。

    ```cpp
    RunMe.cmd infFileName
    ```

    たとえば、次のように入力します。

    ```cpp
    RunMe.cmd myDriver.inf
    ```

    **注**  Device.Graphics テスト スイートは INF ファイルを使いませんが、**RunMe.cmd** スクリプトには INF ファイルが必要です。 必要に応じて代替 INF ファイルの名前を指定できます。

     

## <a name="span-idhck_test_suitesspanspan-idhck_test_suitesspanspan-idhck_test_suitesspanhct-test-suites"></a><span id="HCK_test_suites"></span><span id="hck_test_suites"></span><span id="HCK_TEST_SUITES"></span>HCT テスト スイート


-   [HCK Tests.Basic.Device.Device Fundamentals Test Suite](#HCK_devfund)
-   [HCK Tests.Basic.Device.Graphics Test Suite](#HCK_graphics)
-   [HCK Tests.Basic.Device.Imaging Test Suite](#HCK_imaging)
-   [HCK Tests.Basic.Device.Network.MobileBroadband.CDMA Test Suite](#HCK_CDMA)
-   [HCK Tests.Basic.Device.Network.MobileBroadband.GSM Test Suite](#HCK_GSM)
-   [HCK Tests.Basic.Device.Network.WLAN Test Suite](#HCK_WLAN)

テスト パラメーターの指定について詳しくは、「[Device Fundamental テストのパラメーター](how-to-select-and-configure-the-device-fundamental-tests.md)」を参照してください。 テスト中のデバイスまたはその子デバイスのいずれかが、WiFi アダプターまたはネットワーク デバイスの場合、*Wpa2PskAesSsid*、*Wpa2PskPassword*、または *WDTFREMOTESYSTEM* の各パラメーターの設定が必要なことがあります。

### <a name="span-idhck_devfundspanspan-idhck_devfundspanspan-idhck_devfundspanhck-testsbasicdevicedevice-fundamentals-test-suite"></a><span id="HCK_devfund"></span><span id="hck_devfund"></span><span id="HCK_DEVFUND"></span>HCK Tests.Basic.Device.Device Fundamentals Test Suite

あらゆるデバイスの種類の全般的な信頼性テストを行うには、このテスト スイートを使います。 [Device.Fundamentals の信頼性テストの前提条件](https://go.microsoft.com/fwlink/p/?linkid=309665)に関するページに記載された HCK テストのハードウェア要件、ソフトウェア要件、テスト要件に従う必要があります。 HCK Studio と HCK コントローラーの代わりに、Visual Studio と WDK 8.1 を使って基本的なテストを実行できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Device Fundamentals Test Suite</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ハードウェア要件、ソフトウェア要件、テスト要件</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309665" data-raw-source="[Device.Fundamentals Reliability Testing Prerequisites](https://go.microsoft.com/fwlink/p/?linkid=309665)">Device.Fundamentals の信頼性テストの前提条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>テストの概要</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309669" data-raw-source="[DF - PNP (disable and enable) with IO Before and After (Basic)](https://go.microsoft.com/fwlink/p/?linkid=309669)">DF - 前後の I/O を伴う PNP (無効化/有効化) (基本)</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=309670" data-raw-source="[DF - Sleep with IO Before and After (Basic)](https://go.microsoft.com/fwlink/p/?linkid=309670)">DF - 前後の I/O を伴うスリープ (基本)</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_graphicsspanspan-idhck_graphicsspanspan-idhck_graphicsspanhck-testsbasicdevicegraphics-test-suite"></a><span id="HCK_graphics"></span><span id="hck_graphics"></span><span id="HCK_GRAPHICS"></span>HCK Tests.Basic.Device.Graphics Test Suite

グラフィックス アダプターまたはチップセットをテストするには、このテスト スイートを使います。 [グラフィック アダプターまたはチップセットのテストの前提条件](https://go.microsoft.com/fwlink/p/?linkid=309671)に関するページに記載された HCK テストのハードウェア要件、ソフトウェア要件、テスト要件に従う必要があります。 HCK Studio と HCK コントローラーの代わりに、Visual Studio と WDK 8.1 を使って基本的なテストを実行できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Graphics Test Suite</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ハードウェア要件、ソフトウェア要件、テスト要件</strong></td>
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=309671" data-raw-source="[Graphic Adapter or Chipset Testing Prerequisites](https://go.microsoft.com/fwlink/p/?linkid=309671)">グラフィック アダプターまたはチップセットのテストの前提条件に関するページ</a></td>
</tr>
<tr class="even">
<td align="left"><strong>テストの概要</strong></td>
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=309672" data-raw-source="[Graphic Adapter or Chipset Tests](https://go.microsoft.com/fwlink/p/?linkid=309672)">グラフィック アダプターまたはチップセットのテストに関するページ</a></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_imagingspanspan-idhck_imagingspanspan-idhck_imagingspanhck-testsbasicdeviceimaging-test-suite"></a><span id="HCK_imaging"></span><span id="hck_imaging"></span><span id="HCK_IMAGING"></span>HCK Tests.Basic.Device.Imaging Test Suite

プリンターをテストするには、このテスト スイートを使います。 このテスト スイートでは、HCK [Device.Imaging テスト](https://go.microsoft.com/fwlink/p/?linkid=309673)の一部になっているテストが使われます。 HCK Studio と HCK コントローラーの代わりに、Visual Studio と WDK 8.1 を使って基本的なテストを実行できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Imaging Test Suite</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ハードウェア要件、ソフトウェア要件、テスト要件</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309674" data-raw-source="[Printer Testing Prerequisites](https://go.microsoft.com/fwlink/p/?linkid=309674)">プリンターのテストの前提条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>テストの概要</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309675" data-raw-source="[Printer Tests](https://go.microsoft.com/fwlink/p/?linkid=309675)">プリンター テスト</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_cdmaspanspan-idhck_cdmaspanhck-testsbasicdevicenetworkmobilebroadbandcdma-test-suite"></a><span id="HCK_CDMA"></span><span id="hck_cdma"></span>HCK Tests.Basic.Device.Network.MobileBroadband.CDMA Test Suite

モバイル ブロードバンド CDMA デバイスをテストするには、このテスト スイートを使います。 [モバイル ブロードバンドのテストの前提条件](https://go.microsoft.com/fwlink/p/?linkid=309676)に関するページに記載されたデバイスのセットアップと構成のガイドラインに従います。 HCK Studio と HCK コントローラーの代わりに、Visual Studio と WDK 8.1 を使って基本的なテストを実行できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Network.MobileBroadband.CDMA Test Suite</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ハードウェア要件、ソフトウェア要件、テスト要件</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309676" data-raw-source="[Mobile Broadband Testing Prerequisites](https://go.microsoft.com/fwlink/p/?linkid=309676)">モバイル ブロードバンドのテストの前提条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>テストの概要</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309677" data-raw-source="[CDMA Tests](https://go.microsoft.com/fwlink/p/?linkid=309677)">CDMA テスト</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_gsmspanspan-idhck_gsmspanhck-testsbasicdevicenetworkmobilebroadbandgsm-test-suite"></a><span id="HCK_GSM"></span><span id="hck_gsm"></span>HCK Tests.Basic.Device.Network.MobileBroadband.GSM Test Suite

モバイル ブロードバンド GSM デバイスをテストするには、このテスト スイートを使います。 [モバイル ブロードバンドのテストの前提条件](https://go.microsoft.com/fwlink/p/?linkid=309676)に関するページに記載されたデバイスのセットアップと構成のガイドラインに従います。 HCK Studio と HCK コントローラーの代わりに、Visual Studio と WDK 8.1 を使って基本的なテストを実行できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Network.MobileBroadband.GSM Test Suite</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ハードウェア要件、ソフトウェア要件、テスト要件</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309676" data-raw-source="[Mobile Broadband Testing Prerequisites](https://go.microsoft.com/fwlink/p/?linkid=309676)">モバイル ブロードバンドのテストの前提条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>テストの概要</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309678" data-raw-source="[GSM Tests](https://go.microsoft.com/fwlink/p/?linkid=309678)">GSM テスト</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idhck_wlanspanspan-idhck_wlanspanhck-testsbasicdevicenetworkwlan-test-suite"></a><span id="HCK_WLAN"></span><span id="hck_wlan"></span>HCK Tests.Basic.Device.Network.WLAN Test Suite

ワイヤレス LAN (802.11) デバイスをテストするには、このテスト スイートを使います。 HCK の[ワイヤレス LAN (802.11) のテストの前提条件](https://go.microsoft.com/fwlink/p/?linkid=309679)に関するページに記載されたデバイスのセットアップと構成のガイドラインに従います。 HCK Studio と HCK コントローラーの代わりに、Visual Studio と WDK 8.1 を使って基本的なテストを実行できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HCK Tests.Basic.Device.Network.WLAN Test Suite</th>
<th align="left"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ハードウェア要件、ソフトウェア要件、テスト要件</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309679" data-raw-source="[Wireless LAN (802.11) Testing Prerequisites](https://go.microsoft.com/fwlink/p/?linkid=309679)">ワイヤレス LAN (802.11) のテストの前提条件</a></p></td>
</tr>
<tr class="even">
<td align="left"><strong>テストの概要</strong></td>
<td align="left"><p><a href="https://go.microsoft.com/fwlink/p/?linkid=309680" data-raw-source="[WLAN L1 Tests](https://go.microsoft.com/fwlink/p/?linkid=309680)">WLAN L1 テスト</a></p></td>
</tr>
</tbody>
</table>

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

* [Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)
* [Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)
* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
* [Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)
* [ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227016)
* [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)
* [コマンド プロンプトから実行時にドライバーをテストする方法](how-to-test-a-driver-at-runtime-from-a-command-prompt.md)

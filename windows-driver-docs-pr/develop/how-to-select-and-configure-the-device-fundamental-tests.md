---
ms.assetid: DDAF6D33-46D8-4A04-A3DC-C9FE26ABD003
title: Device Fundamental テストを選んで構成する方法
description: Windows 8 用 WDK には、Device Fundamental テストと呼ばれる一連のテストを含むドライバー テスト フレームワークが用意されています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20842ec8fd3dd48672fe9ea1f7301739c36d00aa
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349145"
---
# <a name="how-to-select-and-configure-the-device-fundamentals-tests"></a>Device Fundamental テストを選んで構成する方法

Windows 8 用 WDK には、Device Fundamental テストと呼ばれる一連のテストを含むドライバー テスト フレームワークが用意されています。 Device Fundamental テストはテストのコレクションで、Windows と WDK に同梱されるドライバーやドライバー サンプルのテスト用に Microsoft 社内で使われることも、[Windows ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=8705)の一環として外部で使われることもあります。 このテストは開発環境から実行できます。 テストを実行するときは、Windows 認定のテストで使ったのと同じパラメーターを使ったり、テストやデバッグのニーズに応じてランタイム パラメーターの構成やカスタマイズを行ったりできます。

## <a name="span-idgettingthemostfromthedevicefundamentalstestsspanspan-idgettingthemostfromthedevicefundamentalstestsspanspan-idgettingthemostfromthedevicefundamentalstestsspangetting-the-most-from-the-device-fundamentals-tests"></a><span id="Getting_the_most_from_the_Device_Fundamentals_tests"></span><span id="getting_the_most_from_the_device_fundamentals_tests"></span><span id="GETTING_THE_MOST_FROM_THE_DEVICE_FUNDAMENTALS_TESTS"></span>Device Fundamental テストの有効活用


Device Fundamental テストを最大限に有効活用するには、デバイスが既定の I/O プラグインでサポートされている必要があります。デバイスの種類がサポートされているかどうかと、テストに固有の要件があるかどうかを確認するには、「[提供されている WDTF シンプル I/O プラグイン](https://msdn.microsoft.com/Library/Windows/Hardware/Hh781398)」をご覧ください。Device Fundamental テストには、デバイスがサポートされているかどうかの確認テストに使うことができるユーティリティも含まれています。 デバイスがサポートされていない場合は、WDTF シンプル I/O プラグインを  Visual Studio で作ることができます。 詳しくは、「[WDTF シンプル I/O アクション プラグインを使ってデバイスの I/O をカスタマイズする方法](https://msdn.microsoft.com/Library/Windows/Hardware/Hh706277)」をご覧ください。

## <a name="span-idaboutthedevicefundamentalstestsspanspan-idaboutthedevicefundamentalstestsspanspan-idaboutthedevicefundamentalstestsspanabout-the-device-fundamentals-tests"></a><span id="About_the_Device_Fundamentals_Tests"></span><span id="about_the_device_fundamentals_tests"></span><span id="ABOUT_THE_DEVICE_FUNDAMENTALS_TESTS"></span>Device Fundamental テストについて


WDK には、"基本" と "認定" の 2 つの構成の Device Fundamental テストが用意されています。 どちらの構成でも、対象のデバイスやドライバーをどのようにテストするかに応じてテスト パラメーターを編集し、テストの長さや実行するテスト サイクルの数などを変えることができます。 基本構成は、一般的なドライバーとデバイスのテストとデバッグを対象としています。 開発サイクルの初期段階とサイクル全体で、基本構成を使います。 基本構成のテストの設定は、実行時間が短いことを除いて、Windows 認定のテストで使う設定と同じです。 認定構成では、テストの設定は Windows 認定のテストで使う設定と同じです。 デバイスやドライバーについて、[Windows ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=8705)のテストの準備が整っているかどうかを確認するには、認定構成を使います。

[Device Fundamental テスト](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673011)には、次のカテゴリのテストが含まれています。

-   [CHAOS テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673008)
-   [カバレッジ テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673009)
-   [CPUStress テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673010)
-   [Driver Install テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673012)
-   [I/O テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673013)
-   [侵入テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673014)
-   [PNP テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673015)
-   [再起動テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673016)
-   [スリープ テスト (Device Fundamental)](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673017)
-   [ユーティリティ](#utility_tests)
-   [ドライバーの検証ツール](#utility_tests)

### <a name="span-idsettingtherun-timetestparametersspanspan-idsettingtherun-timetestparametersspanspan-idsettingtherun-timetestparametersspansetting-the-run-time-test-parameters"></a><span id="Setting_the_run-time_test_parameters"></span><span id="setting_the_run-time_test_parameters"></span><span id="SETTING_THE_RUN-TIME_TEST_PARAMETERS"></span>実行時テスト パラメーターの設定

多くの Device Fundamental テストで、ランタイム パラメーターを編集できます。 [Driver Test Group] (ドライバー テスト グループ) ウィンドウで、テスト名の横に表示される矢印 (») は、そのテストに変更できるパラメーターがあることを示しています。 矢印 (») をクリックして、実行時パラメーターを表示します。

最も有用なパラメーターの 1 つは *DQ* で、テスト対象のデバイスを指定します。 既定値 (**IsDevice**) の場合は、ターゲット コンピューター上のすべてのデバイスがテストされます。 *DQ* パラメーターは、対象のデバイスを特定する [**WDTF**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547) [SDEL](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539571) クエリを受け取ります。 特定のデバイスをテスト対象に指定できます。たとえば、

**DeviceID=’USB\\ROOT\_HUB\\4&1CD5D022&0’** は、**DeviceID** で指定されたデバイスのみをテスト対象として選択します。

*DQ* パラメーターとその他のランタイム パラメーターについて詳しくは、「[Device Fundamental テストのパラメーター](#DevFund_Params)」をご覧ください。

## <a name="span-iddevfundparamsspanspan-iddevfundparamsspanspan-iddevfundparamsspandevice-fundamentals-test-parameters"></a><span id="DevFund_Params"></span><span id="devfund_params"></span><span id="DEVFUND_PARAMS"></span>Device Fundamental テストのパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="DQ"></span><span id="dq"></span><em>DQ</em></p></td>
<td align="left"><p>テストに使うデバイスを特定します。 <em>DQ</em> パラメーターは、対象のデバイスを特定する <a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547" data-raw-source="[&lt;strong&gt;WDTF&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547)"><strong>WDTF</strong></a><a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff539571" data-raw-source="[SDEL](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539571)">SDEL</a> クエリを受け取ります。 このクエリは非常に柔軟で、任意の数のデバイス (1 つのデバイスからシステム内のすべてのデバイスまで) を表すのに使うことができます。</p>
<p>一般的な例:</p>
<p></p>
<dl>
<dt><span id="To_test_all_devices_that_were_installed_with_a_specific_INF_File_"></span><span id="to_test_all_devices_that_were_installed_with_a_specific_inf_file_"></span><span id="TO_TEST_ALL_DEVICES_THAT_WERE_INSTALLED_WITH_A_SPECIFIC_INF_FILE_"></span>特定の INF ファイルを使ってインストールされたすべてのデバイスをテストするには:</dt>
<dd><p><strong>INF::FileName=</strong><em>INF_File_Name</em></p>
<p>例: <strong>INF::OriginalInfFileName='%InfFileName%'</strong></p>
<p>これが既定値です。</p>
</dd>
<dt><span id="To_test_a_device_with_a_specific_Device_Id__"></span><span id="to_test_a_device_with_a_specific_device_id__"></span><span id="TO_TEST_A_DEVICE_WITH_A_SPECIFIC_DEVICE_ID__"></span>特定のデバイス ID を持つデバイスをテストするには: </dt>
<dd><p><strong>DeviceId=’</strong><em>DeviceId</em><strong>’</strong></p>
<p>例: <strong>DeviceID=’USB\ROOT_HUB\4&amp;1CD5D022&amp;0’</strong></p>
</dd>
<dt><span id="_To_test_a_device_with_a_specific_interface_"></span><span id="_to_test_a_device_with_a_specific_interface_"></span><span id="_TO_TEST_A_DEVICE_WITH_A_SPECIFIC_INTERFACE_"></span> 特定のインターフェイスを持つデバイスをテストするには:</dt>
<dd><p><strong>Interfaces::</strong><em>InterfaceGUID</em></p>
</dd>
<dt><span id="To_test_a_device_with_a_specific_driver_letter_"></span><span id="to_test_a_device_with_a_specific_driver_letter_"></span><span id="TO_TEST_A_DEVICE_WITH_A_SPECIFIC_DRIVER_LETTER_"></span>特定のドライブ文字を持つデバイスをテストするには:</dt>
<dd><p><strong>Volume::DriverLetter=’</strong><em>DriveLetter</em><strong>’</strong></p>
<p>例: <strong>Volume::DriverLetter=’c:\’</strong></p>
</dd>
<dt><span id="To_test_a_device_with_a_specific_driver____"></span><span id="to_test_a_device_with_a_specific_driver____"></span><span id="TO_TEST_A_DEVICE_WITH_A_SPECIFIC_DRIVER____"></span>特定のドライバーを持つデバイスをテストするには:</dt>
<dd><p><strong>DriverBinaryNames=</strong><em>mydriver.sys</em></p>
</dd>
<dt><span id="____To_test_all_device_of_a_specific_device_Class___________________"></span><span id="____to_test_all_device_of_a_specific_device_class___________________"></span><span id="____TO_TEST_ALL_DEVICE_OF_A_SPECIFIC_DEVICE_CLASS___________________"></span> 特定のデバイス クラスのすべてのデバイスをテストするには:</dt>
<dd><p>たとえば、<strong>Class=CDROM</strong> は CDROM クラスのすべてのデバイスをテストします。</p>
<p>たとえば、<strong>ClassGUID= {36fc9e60-c465-11cf-8056-444553540000}</strong> は、クラス GUID が指定した GUID と一致するすべてのデバイスをテストします。 この例では、GUID は USB クラスの GUID です。</p>
</dd>
</dl></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DoPoolCheck"></span><span id="dopoolcheck"></span><span id="DOPOOLCHECK"></span><em>DoPoolCheck</em></p></td>
<td align="left"><p>True または False。 プール タグとルックアサイド リストを使って、ドライバーによる ページ システム メモリ プールと非ページ システム メモリ プールの使用状況を監視します。 このオプションを使うと、処理された例外の数の変化 (これは例外処理のエラーを表す場合があります) も監視されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ChangeBufferProtectionFlags"></span><span id="changebufferprotectionflags"></span><span id="CHANGEBUFFERPROTECTIONFLAGS"></span><em>ChangeBufferProtectionFlags</em></p></td>
<td align="left"><p>True または False。 テスト対象のデバイスに渡されたバッファーのメモリ保護フラグを変更します。 メモリ保護フラグは、アクセスなし、読み取り専用、ページ ガードによる読み取り専用のいずれかが適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="DoSimpleIO"></span><span id="dosimpleio"></span><span id="DOSIMPLEIO"></span><em>DoSimpleIO</em></p></td>
<td align="left"><p>True または False。 PNP 操作の実行の前後に、テスト デバイスでシンプル I/O (見つかった場合) を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="DoConcurrentIO"></span><span id="doconcurrentio"></span><span id="DOCONCURRENTIO"></span><em>DoConcurrentIO</em></p></td>
<td align="left"><p>True または False。 <a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547" data-raw-source="[WDTF](https://msdn.microsoft.com/Library/Windows/Hardware/Ff539547)">WDTF</a> 同時 I/O インターフェイスを使って、PNP 操作の実行中に対象のデバイス スタックに I/O 要求を送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="FillZeroPageWithNull"></span><span id="fillzeropagewithnull"></span><span id="FILLZEROPAGEWITHNULL"></span><em>FillZeroPageWithNull</em></p></td>
<td align="left"><p>True または False。 ゼロ ページをマッピングし、NULL 値を入力します。 このテストでは、ポインターを逆参照する前にポインター参照を 検証しないドライバーを特定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="FuzzTestPeriod"></span><span id="fuzztestperiod"></span><span id="FUZZTESTPERIOD"></span><em>FuzzTestPeriod</em></p></td>
<td align="left"><p>ファジー テスト期間 (単位: 分)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="HPU"></span><span id="hpu"></span><em>HPU</em></p></td>
<td align="left"><p>高いプロセッサ使用率の割合を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Impersonate"></span><span id="impersonate"></span><span id="IMPERSONATE"></span><em>Impersonate</em></p></td>
<td align="left"><p>True または False。 管理者特権を持たないユーザーとしてテストを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="IOPeriod"></span><span id="ioperiod"></span><span id="IOPERIOD"></span><em>IOPeriod</em></p></td>
<td align="left"><p>I/O 期間を分単位で指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="IOType"></span><span id="iotype"></span><span id="IOTYPE"></span><em>IOType</em></p></td>
<td align="left"><p>I/O ストレス テストの種類としてSimpleIOStressEx または SimpleIOStressProc (別のプロセスの I/O) を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="LPU"></span><span id="lpu"></span><em>LPU</em></p></td>
<td align="left"><p>低いプロセッサ使用率の割合を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxInBuffer"></span><span id="maxinbuffer"></span><span id="MAXINBUFFER"></span><em>MaxInBuffer</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) でドライバーに渡される入力バッファーの最大サイズをバイト数で指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinInBuffer"></span><span id="mininbuffer"></span><span id="MININBUFFER"></span><em>MinInBuffer</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) でドライバーに渡される入力バッファーの最小サイズをバイト数で指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxOutBuffer"></span><span id="maxoutbuffer"></span><span id="MAXOUTBUFFER"></span><em>MaxOutBuffer</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) でドライバーに渡される出力バッファーの最大サイズをバイト数で指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinOutBuffer"></span><span id="minoutbuffer"></span><span id="MINOUTBUFFER"></span><em>MinOutBuffer</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) でドライバーに渡される出力バッファーの最小サイズをバイト数で指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxRandomCalls"></span><span id="maxrandomcalls"></span><span id="MAXRANDOMCALLS"></span><em>MaxRandomCalls</em></p></td>
<td align="left"><p>テストが発行する呼び出しの最大数を 指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MaxTailoredCalls"></span><span id="maxtailoredcalls"></span><span id="MAXTAILOREDCALLS"></span><em>MaxTailoredCalls</em></p></td>
<td align="left"><p>調整済みランダム テストの際にテストが発行する 呼び出しの最大数を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxDeviceType"></span><span id="maxdevicetype"></span><span id="MAXDEVICETYPE"></span><em>MaxDeviceType</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) 内の DeviceType フィールドの最大値を指定します。 指定できる最大の値は 65535 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinDeviceType"></span><span id="mindevicetype"></span><span id="MINDEVICETYPE"></span><em>MinDeviceType</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) 内の DeviceType フィールドの最小値を指定します。 指定できる最小の値は 0 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MaxFunctionCode"></span><span id="maxfunctioncode"></span><span id="MAXFUNCTIONCODE"></span><em>MaxFunctionCode</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) 内の FunctionCode フィールドの最大値を指定します。 指定できる最大の値は 4095 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="MinFunctionCode"></span><span id="minfunctioncode"></span><span id="MINFUNCTIONCODE"></span><em>MinFunctionCode</em></p></td>
<td align="left"><p>FSCTL (または IOCTL テストの IOCTL) 内の FunctionCode フィールドの最小値を指定します。 指定できる最小の値は 0 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PU"></span><span id="pu"></span><em>PU</em></p></td>
<td align="left"><p>プロセッサ使用率の割合を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PingPongPeriod"></span><span id="pingpongperiod"></span><span id="PINGPONGPERIOD"></span><em>PingPongPeriod</em></p></td>
<td align="left"><p>プロセッサ使用率レベルが高い状態 (HPU) から低い状態 (LPU) まで変化する間のピンポン期間を分単位で指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ResumeDelay"></span><span id="resumedelay"></span><span id="RESUMEDELAY"></span><em>ResumeDelay</em></p></td>
<td align="left"><p>コンピューターがスリープ モードから再開された後、次の I/O サイクルが開始されるまでの遅延時間 (単位: 秒)。 この遅延時間は、デバイスが稼働状態の復元 (ネットワーク カードの IP アドレスの更新など) を行うために必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="TestCycles"></span><span id="testcycles"></span><span id="TESTCYCLES"></span><em>TestCycles</em></p></td>
<td align="left"><p>実行するテスト サイクル (反復) の数を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="WDTFREMOTESYSTEM"></span><span id="wdtfremotesystem"></span><em>WDTFREMOTESYSTEM</em></p></td>
<td align="left"><p>このパラメーターは、テスト中のデバイスまたはその子デバイスのいずれかが、IPv6 ゲートウェイ アドレスを持たない有線ネットワーク アダプターである場合にのみ必要です。 ネットワークでこのパラメーターが必要な場合、テスト ネットワーク アダプターがネットワークをテストするために ping できる IPv6 アドレスを指定する必要があります。</p>
<p>例: <strong>fe80::78b6:810:9c12:46cd</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Wpa2PskAesSsid"></span><span id="wpa2pskaesssid"></span><span id="WPA2PSKAESSSID"></span><em>Wpa2PskAesSsid</em></p></td>
<td align="left"><p>このパラメーターは、テスト中のデバイスまたはその子デバイスのいずれかが、WiFi アダプターである場合にのみ必要です。 テストで WiFi アダプターのテストに使用できる WPA2 AES WiFi ネットワークの SSID を指定します。</p>
<p>既定値: <strong>kitstestssid</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Wpa2PskPassword"></span><span id="wpa2pskpassword"></span><span id="WPA2PSKPASSWORD"></span><em>Wpa2PskPassword</em></p></td>
<td align="left"><p>このパラメーターは、テスト中のデバイスまたはその子デバイスのいずれかが、WiFi アダプターである場合にのみ必要です。 Wpa2PskAesSsid パラメーターを使用して指定された WPA2 AES WiFi ネットワークのパスワードを指定します。</p>
<p>既定値: <strong>password</strong></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idutilitytestsspanspan-idutilitytestsspanutility-tests"></a><span id="utility_tests"></span><span id="UTILITY_TESTS"></span>ユーティリティ テスト


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テスト</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Display_devices_that_have_WDTF_Simple_I_O_plug-ins"></span><span id="display_devices_that_have_wdtf_simple_i_o_plug-ins"></span><span id="DISPLAY_DEVICES_THAT_HAVE_WDTF_SIMPLE_I_O_PLUG-INS"></span>WDTF シンプル I/O プラグインを持つデバイスの表示</p></td>
<td align="left"><p><strong>パラメータ:</strong>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_devices_that_have_Driver_Verifier_enabled"></span><span id="display_devices_that_have_driver_verifier_enabled"></span><span id="DISPLAY_DEVICES_THAT_HAVE_DRIVER_VERIFIER_ENABLED"></span>ドライバーの検証ツールが有効になっているデバイスの表示</p></td>
<td align="left"><p><strong>パラメータ:</strong>なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Display_devices"></span><span id="display_devices"></span><span id="DISPLAY_DEVICES"></span>ディスプレイ デバイス</p></td>
<td align="left"><p><strong>パラメータ:</strong>なし</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddvrftestsspanspan-iddvrftestsspandriver-verifier"></a><span id="dvrf_tests"></span><span id="DVRF_TESTS"></span>ドライバーの検証ツール


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テスト</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Disable_Driver_Verifier"></span><span id="disable_driver_verifier"></span><span id="DISABLE_DRIVER_VERIFIER"></span>Disable Driver Verifier (ドライバーの検証ツールの無効化)</p></td>
<td align="left"><p>テスト コンピューターで<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)">ドライバーの検証ツール</a>を無効にします。</p>
<p><strong>パラメータ:</strong>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Driver_Verifier"></span><span id="enable_driver_verifier"></span><span id="ENABLE_DRIVER_VERIFIER"></span>Enable Driver Verifier (ドライバーの検証ツールの有効化)</p></td>
<td align="left"><p>このテストを使うと、テスト コンピューター上の 1 つ (または複数の) デバイスのドライバーすべてに対して、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)">ドライバーの検証ツール</a>を有効にすることができます。</p>
<p><strong>パラメータ:</strong>- 「<a href="https://msdn.microsoft.com/library/windows/hardware/ff545470" data-raw-source="[Driver Verifier Options](https://msdn.microsoft.com/library/windows/hardware/ff545470)">ドライバーの検証ツールのオプション</a>」をご覧ください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)
* [Device Fundamental のテスト](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673011)
* [提供されている WDTF シンプル I/O プラグイン](https://msdn.microsoft.com/Library/Windows/Hardware/Hh781398)
* [WDTF シンプル I/O アクション プラグインを使ってデバイスの I/O をカスタマイズする方法](https://msdn.microsoft.com/Library/Windows/Hardware/Hh706277)
 

 







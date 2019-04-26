---
title: PnP テスト (Device Fundamental)
description: デバイスの基礎 PnP テスト PnP Irp; のほぼすべてを処理するためのドライバーを強制します。ただしが具体的には、削除、再調整、および突然の取り外しは 3 つの領域が強調されます。
ms.assetid: 4224F92B-5430-4F55-900D-0B08ADBE54F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6a7d773b8c5111dd7577db676e4f09aa8e0b688
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356304"
---
# <a name="pnp-tests-device-fundamentals"></a>PnP テスト (Device Fundamental)


デバイスの基礎 PnP テスト PnP Irp; のほぼすべてを処理するためのドライバーを強制します。ただし、具体的には負荷がかかっている 3 つの領域がある: 削除、再調整、および突然の削除。 PnP テストは、これらのそれぞれを個別に、テスト、またはすべて同時にテストするメカニズムを提供します (これは、ストレス テストとして)。 PnP このテストは、ユーザー モード API の呼び出し (のテスト アプリケーションの概要) と (上位フィルター ドライバー) を通じてカーネル モードの API 呼び出しの組み合わせを使用して行われます。

## <a name="pnp-tests"></a>PNP テスト


プラグ アンド プレイ (PnP) テストでは、ドライバーとユーザー モード コンポーネントでさまざまな PnP に関連するコード パスを実行します。 PnP のテストが実行する必要があります[Driver Verifier](driver-verifier.md)テスト コンピューターで有効にします。 ドライバーの検証を有効にする方法については、次を参照してください。[ドライバー プロジェクトの Driver Verifier プロパティ](https://msdn.microsoft.com/windows-drivers/develop/driver_verifier_properties_for__driver_projects)します。

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
<td align="left"><p><span id="Disable_Enhanced_Device_Testing__EDT__Support_"></span><span id="disable_enhanced_device_testing__edt__support_"></span><span id="DISABLE_ENHANCED_DEVICE_TESTING__EDT__SUPPORT_"></span>テスト (EDT) サポート、強化されたデバイスを無効にします。</p></td>
<td align="left"><p>このテストでは、DQ パラメーターを使用して指定したデバイスの上限をフィルターとして、テスト フィルター ドライバー (msdmfilt.sys) をアンインストールします。 このテストのフィルターは、このテスト カテゴリのテストの実行の一部としてインストールを取得します</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP__disable_and_enable__reboot_with_IO_before_and_after"></span><span id="pnp__disable_and_enable__reboot_with_io_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__REBOOT_WITH_IO_BEFORE_AND_AFTER"></span>PNP (無効および有効にする) で再起動 IO 前に、と後</p></td>
<td align="left"><p>このテストは、システムの再起動を備えたデバイスでの基本的な PnP の無効化/有効化と I/O を実行します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PNP_DisableEnable_Reboot_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>PNP_DisableEnable_Reboot_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP__disable_and_enable__with_I_O_before_and_after"></span><span id="pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>PNP (無効および有効にする) I/O を前に、と後</p></td>
<td align="left"><p>このテストは、デバイスの I/O と基本的な PnP の無効化/有効化を実行します。</p>
<p>このテストは、次を行います。</p>
<ol>
<li>デバイスの問題のコードをレポート作成システム上のデバイスがないことを確認します。</li>
<li>WDTF 単純な I/O プラグインを使用して、システム上のすべてのデバイスで I/O をテストします。 参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/hh781398" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/library/windows/hardware/hh781398)">WDTF の単純な I/O を提供するプラグイン</a>詳細についてはします。</li>
<li>WDTF PnP アクションのインターフェイスを使用して、システム上のすべてのデバイスを参照してください有効と無効になります<a href="https://msdn.microsoft.com/library/windows/hardware/hh451068" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::DisableDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451068)"> <strong>IWDTFPNPAction2::DisableDevice</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/hh451082" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::EnableDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451082)"> <strong>IWDTFPNPAction2::EnableDevice</strong> </a>方法の詳細について。</li>
<li>デバイスの問題のコードをレポート作成システム上のデバイスがないことを確認します。</li>
<li>WDTF 単純な I/O プラグインを使用して、システム上のすべてのデバイスで I/O をテストします。 参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/hh781398" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://msdn.microsoft.com/library/windows/hardware/hh781398)">WDTF の単純な I/O を提供するプラグイン</a>詳細についてはします。</li>
<li>手順 3 ~ 5 を複数回繰り返されます。</li>
</ol>
<p><strong>バイナリをテストします。</strong>Devfund_PNP_DisableEnable_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Cancel_Remove_Device_test_"></span><span id="pnp_cancel_remove_device_test_"></span><span id="PNP_CANCEL_REMOVE_DEVICE_TEST_"></span>PNP デバイスの削除の取り消しのテスト</p></td>
<td align="left"><p>このテストでは、EDT フィルター ドライバーを使用して、ターゲット デバイス スタックを IRP_MN_CANCEL_REMOVE_DEVICE を送信します。</p>
<p>詳細については、次を参照してください。 <a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">、デバイスの削除に関するテスト</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPCancelRemoveDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Cancel_Stop_Device_test"></span><span id="pnp_cancel_stop_device_test"></span><span id="PNP_CANCEL_STOP_DEVICE_TEST"></span>PNP キャンセル停止デバイス テスト</p></td>
<td align="left"><p>このテストでは、EDT フィルター ドライバーを使用して、ターゲット デバイス スタックを IRP_MN_CANCEL_STOP_DEVICE を送信します。</p>
<p>詳細については、次を参照してください。<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストについて、再調整</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPCancelStopDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_DIF_Remove_Device_Test"></span><span id="pnp_dif_remove_device_test"></span><span id="PNP_DIF_REMOVE_DEVICE_TEST"></span>PNP DIF 削除デバイス テスト</p></td>
<td align="left"><p>このテストでは、SetupDi API を使用して、送信、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff543717" data-raw-source="[&lt;strong&gt;DIF_REMOVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543717)"> <strong>DIF_REMOVE</strong> </a>デバイスを削除するインストーラーを要求します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPDIFRemoveAndRescanParentDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Disable_and_Enable_Device_test_"></span><span id="pnp_disable_and_enable_device_test_"></span><span id="PNP_DISABLE_AND_ENABLE_DEVICE_TEST_"></span>PNP 無効および有効にするデバイスのテスト</p></td>
<td align="left"><p>このテストは無効にし、ターゲット デバイスを使用します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPDisableAndEnableDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Rebalance_Fail_Restart_Device_test"></span><span id="pnp_rebalance_fail_restart_device_test"></span><span id="PNP_REBALANCE_FAIL_RESTART_DEVICE_TEST"></span>PNP が失敗する再起動のデバイスの再調整のテスト</p></td>
<td align="left"><p>このテストでは、EDT フィルター ドライバーを使用して、ターゲット デバイス スタックを IRP_MN_STOP_DEVICE を送信しようとしています。 EDT フィルター ドライバーでは、ターゲット デバイスの突然の削除をトリガーする (続く IRP_MN_STOP_DEVICE 要求) IRP_MN_START_DEVICE 要求、失敗します。</p>
<p>詳細については、次を参照してください。<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストについて、再調整</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPTryStopDeviceAndFailRestart</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Rebalance_Request_New_Resources_Device_test"></span><span id="pnp_rebalance_request_new_resources_device_test"></span><span id="PNP_REBALANCE_REQUEST_NEW_RESOURCES_DEVICE_TEST"></span>PNP の新しいリソースの要求を再調整デバイス テスト</p></td>
<td align="left"><p>このテストでは、EDT フィルター ドライバーを使用して、ターゲット デバイス スタックを IRP_MN_STOP_DEVICE を送信しようとしています。 また、新しいリソースがデバイスに割り当てられている確率を最大化するデバイスのリソース要件を操作します。</p>
<p>詳細については、次を参照してください。<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストについて、再調整</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPTryStopDeviceRequestNewResourcesAndRestartDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Remove_Device_Test"></span><span id="pnp_remove_device_test"></span><span id="PNP_REMOVE_DEVICE_TEST"></span>削除の PNP デバイスのテスト</p></td>
<td align="left"><p>このテストによって、IRP_MN_QUERY_REMOVE_DEVICE および IRP_MN_REMOVE_DEVICE デバイス スタックをターゲットに送信されます。</p>
<p>詳細については、次を参照してください。 <a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">、デバイスの削除に関するテスト</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPRemoveAndRestartDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Stop__Rebalance__Device_test"></span><span id="pnp_stop__rebalance__device_test"></span><span id="PNP_STOP__REBALANCE__DEVICE_TEST"></span>PNP デバイスの停止 (再調整) のテスト</p></td>
<td align="left"><p>このテストでは、EDT フィルター ドライバーを使用して、ターゲット デバイス スタックを IRP_MN_STOP_DEVICE を送信しようとしています。</p>
<p>詳細については、次を参照してください。<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストについて、再調整</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPTryStopAndRestartDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Surprise_Remove_Device_test"></span><span id="pnp_surprise_remove_device_test"></span><span id="PNP_SURPRISE_REMOVE_DEVICE_TEST"></span>PNP デバイスの削除の突然のテスト</p></td>
<td align="left"><p>このテストでは、EDT フィルター ドライバーを使用して、ターゲット デバイス スタックを IRP_MN_SURPRISE_REMOVAL を送信します。</p>
<p>詳細については、次を参照してください。<a href="#about-the-surprise-removal-test" data-raw-source="[About the Surprise Removal test](#about-the-surprise-removal-test)">突然についての取り外しテスト</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_PnPDTest.dll</p>
<p><strong>メソッドをテストします。</strong>PNPSurpriseRemoveAndRestartDevice</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>DoConcurrentIO</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-device-removal-tests"></a>デバイスの削除のテストについて


- 削除の PNP デバイスのテスト
- PNP デバイスの削除の取り消しのテスト

デバイスの削除のテストは IRP\_MN\_クエリ\_削除\_デバイス、IRP\_MN\_キャンセル\_削除\_デバイス、および IRP\_MN\_削除\_デバイス。

テストは、ターゲット デバイス スタック上に上位フィルター ドライバーをインストールしようとします。 この試行は、クエリの削除の IRP で発生します。

このクエリの削除の IRP に失敗した場合、テストは、デバイス スタックに、フィルター ドライバーを取得するコンピューターを再起動します。 削除要求は拒否されませんが、デバイス スタックが削除され、再起動されると、デバイス スタック上のフィルター ドライバー。

テストには、セットアップ Api を使用して、デバイス スタックに送信されるクエリの削除 IRP をによりします。 フィルター ドライバーでは、[キャンセル] 削除 IRP が送信されるよう、この削除要求が失敗します。 フィルター ドライバーでは、キャンセルと削除が成功したことをアサートします。

次に、テスト アプリケーションを呼び出す、適切なクラスのインストーラーと登録を無効または有効にして削除またはデバイスを再列挙共同インストーラー (差分のクラスおよび共同インストーラーの処理をテスト\_DICSでPROPERTYCHANGE\_無効、DICS\_有効化、および DICS\_PROPCHANGE)。 IRP を受信するときに\_MN\_削除\_デバイス、フィルター ドライバーはアサートにいる下位のドライバーが正常に完了しました。

これらの各手順には、予備の削除要求が含まれます。 その要求が拒否される場合、デバイスは削除されません。 ターゲット デバイスがブートまたはページングのパスの場合、USB カメラでビデオをストリーミング中など、必要に応じて、または削除要求を拒否を選択することができます。 単に、失敗したすべての削除要求が一般にないことをお勧めしてください。 すべての削除失敗した要求は保証されません削除 IRP がまだ発行されます突然の削除後になっているか、開始 IRP デバイス スタック内のだれもが失敗した場合は、ドライバーは、削除を受け取りません。

## <a name="about-the-surprise-removal-test"></a>テストの突然の削除に関する


- PNP デバイスの削除の突然のテスト

テストの突然の取り外しは IRP\_MN\_突然\_IRP の後に削除\_MN\_削除\_デバイス。

として前のテストでテスト アプリケーションはしようとすると、ターゲット デバイス スタックを上位のフィルターを追加し、スタックを再起動します。 この試行が成功しなかった場合、テストは、コンピューターを再起動します。

フィルター ドライバーは IRP を送信するシステムと、テスト アプリケーションによってトリガーされると、\_MN\_突然\_IRP の後に削除、デバイス スタックを\_MN\_削除\_デバイスです。 フィルター ドライバーは、これら Irp の両方の下位のドライバーによってが正常に完了がアサートします。

デバイスをアンインストールして、再度列挙、突然の削除のテストが完了した後も、フィルター ドライバーをスタックから削除します。

## <a name="about-the-rebalance-tests"></a>再調整テストについて


- PNP デバイスの停止 (再調整) のテスト
- PNP の新しいリソースの要求を再調整デバイス テスト
- PNP が失敗する再起動のデバイスの再調整のテスト
- PNP キャンセル停止デバイス テスト

削除、テストと同様、テスト アプリケーションが、ターゲット デバイス スタックを上位のフィルターを追加しを使用して、デバイス スタックを再開を試みます**SetupDiCallClassInstaller**差分と\_PROPERTYCHANGE します。 場合この試行が失敗したは、(つまり、ターゲット デバイス スタック上のユーザーが IRP がクエリの削除に失敗しました) 場合、テストが再調整をテストするコンピューターを再起動します。

によって再調整テストを選択することで、次のイベントが発生します。

1.  **PNP デバイスの停止 (再調整) テスト**このテストの開始 IRP が再調整プロシージャ\_MN\_クエリ\_停止\_デバイス ドライバーの PnP IRP のデバイス。

    スタック内の任意のドライバーには、この IRP が失敗した場合、再調整の手順は破棄されます。 Windows Vista では複数レベルの再調整のサポートに注意してください。 再調整は、デバイスの非リーフ ノードで開始されている場合、ルートとしているデバイス ノードで、デバイス ツリーに存在するデバイス スタックのすべても経由再調整します。 子デバイス スタックのいずれかには、クエリの停止が失敗した場合、全体の再調整プロシージャが破棄されます。 このため、ドライバーでは、正規品である理由なくクエリの停止が失敗する必要があります。 PnP マネージャーがキャンセルの停止を送信してこのエラーが発生した場合 (IRP\_MN\_キャンセル\_停止) するとクエリの停止が送信されていたすべてのデバイス スタック。

    クエリの停止を渡すすべての関連するデバイス スタックの場合、テストは、再調整を続行され、IRP を送信します\_MN\_クエリ\_リソース\_要件と IRP\_MN\_フィルター\_リソース\_要件 IRP のデバイスのリソース要件が見つかりません。

    この時点で後、は、2 つの異なるパスがターゲット デバイスがすべてのリソースを消費するかどうかどうかに応じて考えられます。

    -   PnP マネージャー自体がキャンセル停止を送信する場合は、デバイスでは、すべてのリソースを消費しません (IRP\_MN\_キャンセル\_停止\_デバイス)、最適化として。

        IRP に再調整プロシージャが終了する場合は、デバイスは、実際には、リソースを消費する\_MN\_停止\_デバイスと IRP\_MN\_開始\_Irp のデバイス。

    このオプションで、デバイスのリソースは変更されません。

2.  **PNP キャンセル停止デバイス テスト**:このテストを再調整の手順を開始しますが、フィルター ドライバーは、クエリ停止 IRP を意図的に失敗します。 Irp の順序の IRP よう\_MN\_クエリ\_停止\_(これは再調整の取り消しの原因を受信中に、フィルター ドライバーによって失敗) デバイスと IRP\_MN\_キャンセル\_停止\_デバイス。

    このオプションで、デバイスのリソースを変更しないでください。

3.  **PNP の新しいリソースの要求を再調整デバイス テスト**このテストを再調整を開始しても実際に新しいリソースがデバイスに割り当てられている確率を最大化するデバイスのリソース要件を操作します。 このオプションは、実際には、完全な再調整の手順を経由するリソースがデバイスにも役立ちません。
    1.  単純な再調整を開始、まず、次の Irp の原因します。
        -   IRP\_MN\_クエリ\_停止\_デバイス (この IRP がすべてのドライバーによって渡されると仮定します。 テストの既に説明がこの IRP が失敗した場合。)
        -   IRP\_MN\_クエリ\_リソース\_要件
        -   IRP\_MN\_フィルター\_リソース\_要件。 移動中に、この IRP への応答フィルター ドライバーは、デバイスがすべてのリソースを消費するかどうかどうかに基づいてアクションを受け取ります。
            -   リソース要件、デバイスがない場合は、フィルターが偽のリソースを割り当てます。
            -   デバイスがリソース要件を持つ場合、現在の割り当てを変更する確率を最大化するように、リソース要件の一覧を再構築しようとします。 たとえば、デバイスが 00 ~ FF の任意の場所間のメモリは 2 バイト必要現在 3 a 3 b が割り当てられている場合は、(優先順) に新しいリソースの要件が 00 39 または 3 C FF 3A 3B のようになるように変更します。 同様に、デバイスのリソース要件の一覧に、代替の要件がある場合は、代替の要件が既にリストでは、その順序が変更されます。

    2.  これで、デバイスでは、再調整手順が完了常にする必要があります。

        IRP\_MN\_停止\_デバイス

        IRP\_MN\_開始\_デバイス (新しい割り当てられているリソース。 偽の要件は、作成された場合のマスク実際ドライバーから新しいリソースです。)

4.  **PNP を再調整が失敗する再起動デバイス テスト**このテストを再調整を開始しますが、削除 IRP IRP の突然の削除後に it がある原因が意図的に、フィルター ドライバーでは、開始を取得後、再調整と、失敗します。

    最初に、再調整プロシージャを開始し、により、ドライバーですべてのリソースを消費しないデバイス用の偽のリソース要件を生成することで、停止および開始を取得します。

    -   IRP\_MN\_クエリ\_停止\_デバイス (この IRP がすべてのドライバーによって渡されると仮定します。 テストの既に説明がこの IRP が失敗した場合。)
    -   IRP\_MN\_クエリ\_リソース\_要件
    -   IRP\_MN\_フィルター\_リソース\_要件 (実際のリソース要件が null の場合は、フィルター割り当てる偽のリソースの要件を停止および開始があるため)。
    -   IRP\_MN\_停止\_デバイス
    -   IRP\_MN\_開始\_デバイス (フィルターは、この IRP をするときに失敗します。 この操作により、突然削除 IRP。)
    -   IRP\_MN\_SURPRISE\_REMOVAL
    -   IRP\_MN\_削除

    デバイスをアンインストールして、再度列挙、テストの再調整が完了した後も、フィルター ドライバーをスタックから削除します。

## <a name="device-error-codes"></a>デバイスのエラー コード


テストには、デバイスの状態が OK でないというエラー メッセージが利用できますが場合、できる詳細を確認するデバイスの状態のデバイス マネージャーを使用します。 さまざまなデバイスのエラー コードの概要については、次を参照してください。[デバイス マネージャーのエラー メッセージ](https://msdn.microsoft.com/library/windows/hardware/ff541422)します。

## <a name="debug-installation-failures-using-the-setup-api-logs"></a>API のセットアップ ログを使用して、インストール エラーをデバッグします。


(Setupapi.app.log および setupapi.dev.log) API のセットアップ ログには、このテストで記録されたドライバーのインストール エラーのデバッグに役立つ情報が含まれます。 API のセットアップ ログは %windir% あります\\inf\\テスト システムのディレクトリ。

詳細およびこれらのログの潜在的な有用性を向上させるのには、テストの再インストールを実行する前に次のレジストリ キーを 0x2000FFFF に設定します。

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="related-topics"></a>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供されている WDTF シンプル I/O プラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 







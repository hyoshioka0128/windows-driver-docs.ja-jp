---
title: PnP テスト (デバイスの基礎)
description: デバイスの基本 PnP テストでは、ドライバーがほぼすべての PnP Irp を処理するように強制します。ただし、明確な削除、再調整、および驚くべき削除という3つの領域があります。
ms.assetid: 4224F92B-5430-4F55-900D-0B08ADBE54F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61f6b6db5523925a4e8d3514e5f540e54111cd26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840055"
---
# <a name="pnp-tests-device-fundamentals"></a>PnP テスト (デバイスの基礎)


デバイスの基本 PnP テストでは、ドライバーがほぼすべての PnP Irp を処理するように強制します。ただし、特に、削除、再調整、および驚くべき削除という3つの領域があります。 PnP テストでは、これらを個別にテストするメカニズム、またはすべてをまとめてテストする (つまり、ストレステストとして) ことができます。 この PnP テストは、(テストアプリケーションを通じて) ユーザーモード API 呼び出しとカーネルモード API 呼び出し (上位フィルタードライバーを使用) の組み合わせを使用して実現されます。

## <a name="pnp-tests"></a>PNP テスト


プラグアンドプレイ (PnP) テストでは、ドライバーおよびユーザーモードコンポーネントでさまざまな PnP 関連のコードパスを実行します。 テストコンピューターで[ドライバー検証ツール](driver-verifier.md)が有効になっている状態で、PnP テストを実行する必要があります。 ドライバーの検証機能の有効化の詳細については、「ドライバー[プロジェクトのドライバーの検証ツールのプロパティ](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

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
<td align="left"><p><span id="Disable_Enhanced_Device_Testing__EDT__Support_"></span><span id="disable_enhanced_device_testing__edt__support_"></span><span id="DISABLE_ENHANCED_DEVICE_TESTING__EDT__SUPPORT_"></span>拡張デバイステスト (EDT) のサポートを無効にする</p></td>
<td align="left"><p>このテストは、DQ パラメーターを使用して指定されたデバイスの上位フィルターとして、テストフィルタードライバー (msdmfilt) をアンインストールします。 このテストフィルターは、このテストカテゴリで実行中のテストの一部としてインストールされます</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP__disable_and_enable__reboot_with_IO_before_and_after"></span><span id="pnp__disable_and_enable__reboot_with_io_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__REBOOT_WITH_IO_BEFORE_AND_AFTER"></span>PNP (無効化および有効化) の前後の IO での再起動</p></td>
<td align="left"><p>このテストでは、システムの再起動により、デバイスで基本的な PnP の無効化/有効化と i/o が実行されます。</p>
<p><strong>テストバイナリ:</strong>Devfund_PNP_DisableEnable_Reboot_With_IO_BeforeAndAfter</p>
<p><strong>テストメソッド:</strong>PNP_DisableEnable_Reboot_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP__disable_and_enable__with_I_O_before_and_after"></span><span id="pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>PNP (disable および enable) と i/o の前後の i/o</p></td>
<td align="left"><p>このテストでは、デバイスで i/o と基本的な PnP の無効化/有効化を実行します。</p>
<p>このテストは次のことを行います。</p>
<ol>
<li>システムレポートデバイスの問題コードにデバイスがないことを確認します。</li>
<li>WDTF Simple i/o プラグインを使用して、システム上のすべてのデバイスで i/o をテストします。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)">WDTF Simple i/o プラグインの提供</a>」を参照してください。</li>
<li>WDTF PnP action インターフェイスを使用して、システム上のすべてのデバイスを無効にして有効にします。詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-disabledevice" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::DisableDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-disabledevice)"><strong>IWDTFPNPAction2::D isableDevice</strong></a> 」と「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-enabledevice" data-raw-source="[&lt;strong&gt;IWDTFPNPAction2::EnableDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-enabledevice)"><strong>IWDTFPNPAction2:: enabledevice</strong></a>メソッド」を参照してください。</li>
<li>システムレポートデバイスの問題コードにデバイスがないことを確認します。</li>
<li>WDTF Simple i/o プラグインを使用して、システム上のすべてのデバイスで i/o をテストします。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins" data-raw-source="[Provided WDTF Simple I/O plug-ins](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)">WDTF Simple i/o プラグインの提供</a>」を参照してください。</li>
<li>手順3-5 を何度か繰り返します。</li>
</ol>
<p><strong>テストバイナリ:</strong>Devfund_PNP_DisableEnable_With_IO_BeforeAndAfter</p>
<p><strong>テストメソッド:</strong>PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Cancel_Remove_Device_test_"></span><span id="pnp_cancel_remove_device_test_"></span><span id="PNP_CANCEL_REMOVE_DEVICE_TEST_"></span>PNP によるデバイステストの削除の取り消し</p></td>
<td align="left"><p>このテストでは、EDT フィルタードライバーを使用して、ターゲットデバイススタックに IRP_MN_CANCEL_REMOVE_DEVICE を送信します。</p>
<p>詳細については、「<a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">デバイスの削除テストについ</a>て」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPCancelRemoveDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Cancel_Stop_Device_test"></span><span id="pnp_cancel_stop_device_test"></span><span id="PNP_CANCEL_STOP_DEVICE_TEST"></span>PNP キャンセルのデバイステストの停止</p></td>
<td align="left"><p>このテストでは、EDT フィルタードライバーを使用して、ターゲットデバイススタックに IRP_MN_CANCEL_STOP_DEVICE を送信します。</p>
<p>詳細については、「<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストの再調整について</a>」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPCancelStopDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_DIF_Remove_Device_Test"></span><span id="pnp_dif_remove_device_test"></span><span id="PNP_DIF_REMOVE_DEVICE_TEST"></span>PNP 差分のデバイステストの削除</p></td>
<td align="left"><p>このテストでは、SetupDi API を使用して、インストーラーの<a href="https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove" data-raw-source="[&lt;strong&gt;DIF_REMOVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove)"><strong>DIF_REMOVE</strong></a>要求を送信し、デバイスを削除します。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPDIFRemoveAndRescanParentDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Disable_and_Enable_Device_test_"></span><span id="pnp_disable_and_enable_device_test_"></span><span id="PNP_DISABLE_AND_ENABLE_DEVICE_TEST_"></span>PNP デバイステストを無効にして有効にする</p></td>
<td align="left"><p>このテストでは、ターゲットデバイスを無効にして有効にします。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPDisableAndEnableDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Rebalance_Fail_Restart_Device_test"></span><span id="pnp_rebalance_fail_restart_device_test"></span><span id="PNP_REBALANCE_FAIL_RESTART_DEVICE_TEST"></span>PNP 再調整失敗デバイステスト</p></td>
<td align="left"><p>このテストでは、EDT フィルタードライバーを使用して、ターゲットデバイススタックに IRP_MN_STOP_DEVICE を送信しようとします。 その後、EDT フィルタードライバーは、IRP_MN_START_DEVICE 要求 (IRP_MN_STOP_DEVICE 要求に従う) が失敗し、ターゲットデバイスの突然の削除をトリガーします。</p>
<p>詳細については、「<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストの再調整について</a>」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPTryStopDeviceAndFailRestart</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Rebalance_Request_New_Resources_Device_test"></span><span id="pnp_rebalance_request_new_resources_device_test"></span><span id="PNP_REBALANCE_REQUEST_NEW_RESOURCES_DEVICE_TEST"></span>PNP 再調整要求の新しいリソースのデバイステスト</p></td>
<td align="left"><p>このテストでは、EDT フィルタードライバーを使用して、ターゲットデバイススタックに IRP_MN_STOP_DEVICE を送信しようとします。 また、デバイスのリソース要件を操作して、デバイスに新しいリソースが割り当てられる可能性を最大化します。</p>
<p>詳細については、「<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストの再調整について</a>」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPTryStopDeviceRequestNewResourcesAndRestartDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Remove_Device_Test"></span><span id="pnp_remove_device_test"></span><span id="PNP_REMOVE_DEVICE_TEST"></span>PNP デバイステストの削除</p></td>
<td align="left"><p>このテストによって、IRP_MN_QUERY_REMOVE_DEVICE と IRP_MN_REMOVE_DEVICE がターゲットデバイススタックに送信されます。</p>
<p>詳細については、「<a href="#about-the-device-removal-tests" data-raw-source="[About the Device Removal tests](#about-the-device-removal-tests)">デバイスの削除テストについ</a>て」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPRemoveAndRestartDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="PNP_Stop__Rebalance__Device_test"></span><span id="pnp_stop__rebalance__device_test"></span><span id="PNP_STOP__REBALANCE__DEVICE_TEST"></span>PNP 停止 (再調整) デバイステスト</p></td>
<td align="left"><p>このテストでは、EDT フィルタードライバーを使用して、ターゲットデバイススタックに IRP_MN_STOP_DEVICE を送信しようとします。</p>
<p>詳細については、「<a href="#about-the-rebalance-tests" data-raw-source="[About the Rebalance tests](#about-the-rebalance-tests)">テストの再調整について</a>」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPTryStopAndRestartDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PNP_Surprise_Remove_Device_test"></span><span id="pnp_surprise_remove_device_test"></span><span id="PNP_SURPRISE_REMOVE_DEVICE_TEST"></span>PNP の突然のデバイステストの削除</p></td>
<td align="left"><p>このテストでは、EDT フィルタードライバーを使用して、ターゲットデバイススタックに IRP_MN_SURPRISE_REMOVAL を送信します。</p>
<p>詳細については、「<a href="#about-the-surprise-removal-test" data-raw-source="[About the Surprise Removal test](#about-the-surprise-removal-test)">突然の削除のテストについ</a>て」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_PnPDTest</p>
<p><strong>テストメソッド:</strong>PNPSurpriseRemoveAndRestartDevice</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>DoSimpleIO</em></p>
<p><em>IOPeriod</em></p>
<p><em>Doconon Entio</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-device-removal-tests"></a>デバイスの削除テストについて


- PNP デバイステストの削除
- PNP によるデバイステストの削除の取り消し

デバイスの削除テストでは、IRP\_\_によって、\_デバイスの削除\_デバイスの削除、IRP\_\_\_の削除\_\_デバイスの削除\_\_デバイスの削除の削除が含まれます。

テストでは、ターゲットデバイススタックに上位フィルタードライバーをインストールしようとします。 この試行により、クエリ削除の IRP が生成されます。

このクエリ削除の IRP が失敗した場合、テストによってコンピューターが再起動され、フィルタードライバーがデバイススタックに取得されます。 削除要求が拒否されていない場合、デバイススタックは削除され、デバイススタックのフィルタードライバーを使用して再起動されます。

テストでは、セットアップ Api を使用して、クエリ削除の IRP をデバイススタックに送信します。 フィルタードライバーがこの削除要求に失敗したため、削除の取り消しの IRP が送信されます。 フィルタードライバーは、取り消しが正常に終了したことをアサートします。

次に、適切なクラスインストーラーと登録されているすべての共同インストーラーを呼び出して、デバイスを無効または有効にしたり、reenumerate したりします (これにより、差分\_PROPERTYCHANGE を使用したクラスと共同インストーラーの処理がテストされ\_DISABLE、DICS\_ENABLE、および DICS\_PROPCHANGE)。 \_IRP を受信し\_デバイス\_削除すると、フィルタードライバーは、下位のドライバーが正常に完了したことをアサートします。

これらの各手順には、暫定的な削除要求が含まれます。 要求が拒否された場合、デバイスは削除されません。 USB カメラでビデオをストリーミングしているときや、ターゲットデバイスがブートパスまたはページングパスにある場合など、必要に応じて削除要求を拒否することを選択できます。 すべての削除要求を失敗させるだけでは、一般的には適切な方法ではないことに注意してください。 すべての削除要求が失敗しても、突然削除された後に削除の IRP が発行されること、またはデバイススタック内のすべてのユーザーが start IRP に失敗した場合に、ドライバーが削除を受信しないことは保証されません。

## <a name="about-the-surprise-removal-test"></a>突然の削除テストについて


- PNP の突然のデバイステストの削除

突然の削除テストでは、\_予期しない IRP\_が含まれています。これにより、IRP\_\_\_デバイス\_削除されます。

前のテストと同様に、テストアプリケーションは、ターゲットデバイススタックに上位フィルターを追加し、スタックを再起動しようとします。 この試行が成功しなかった場合、テストによってコンピューターが再起動されます。

テストアプリケーションによってトリガーされた場合、フィルタードライバーによって、システムによって、IRP\_\_、デバイススタックに予期しない\_削除が送信され、その後、\_デバイスの削除\_\_IRP が送信されます。 フィルタードライバーは、これらの両方の Irp が下位のドライバーによって正常に完了したことをアサートします。

予期しない削除のテストが完了すると、デバイスがアンインストールされ、再列挙されます。また、フィルタードライバーもスタックから削除されます。

## <a name="about-the-rebalance-tests"></a>再調整テストについて


- PNP 停止 (再調整) デバイステスト
- PNP 再調整要求の新しいリソースのデバイステスト
- PNP 再調整失敗デバイステスト
- PNP キャンセルのデバイステストの停止

削除テストと同様に、テストアプリケーションは、ターゲットデバイススタックに上位フィルターを追加し、差分\_PROPERTYCHANGE で**Setupdicallclassinstaller**を使用してデバイススタックを再起動しようとします。 この試行が成功しなかった場合 (つまり、ターゲットデバイススタック上のだれかがクエリ削除の IRP に失敗した場合)、テストは再調整のためにコンピューターを再起動します。

選択した再バランステストに応じて、次のイベントが発生します。

1.  **PNP 停止 (再調整) デバイステスト**このテストでは再調整手順を開始します。これにより、IRP\_\_クエリ\_デバイスドライバーへの\_デバイスの PnP IRP が停止します。

    スタック内のいずれかのドライバーで障害が発生した場合、この IRP は再調整手順を破棄します。 Windows Vista では、複数レベルの再調整がサポートされていることに注意してください。 非リーフデバイスノードで再調整が開始された場合、そのデバイスノードがルートとして使用されているデバイスツリーに存在するすべてのデバイススタックも再調整を実行します。 また、子デバイスのスタックのいずれかがクエリの停止に失敗した場合は、再調整手順全体が破棄されます。 そのため、ドライバーは、正規の理由を伴わずにクエリを停止することはできません。 このエラーが発生した場合、PnP マネージャーは、送信されたクエリの停止のすべてのデバイススタックにキャンセル停止 (IRP\_完了\_キャンセル\_停止) を送信します。

    使用されているすべてのデバイススタックがクエリを停止した場合、テストは再調整を続行し、IRP\_\_クエリ\_リソース\_要件と IRP\_\_フィルター\_リソース\_要件を送信します。デバイスのリソース要件を見つけるための IRP。

    この時点以降、ターゲットデバイスがリソースを使用するかどうかに応じて、2つの異なるパスを使用できます。

    -   デバイスがリソースを消費しない場合は、PnP マネージャー自体がキャンセル停止 (IRP\_\_キャンセル\_\_デバイスの停止) を最適化として送信します。

        デバイスが実際にリソースを消費している場合は、IRP\_\_停止\_デバイスと IRP\_、\_デバイスの Irp を開始\_開始することで、再調整手順が完了します。

    このオプションを使用すると、デバイスのリソースが変更されません。

2.  **PNP キャンセルデバイステストの停止**: このテストは再調整手順を開始しますが、フィルタードライバーはクエリ停止 IRP を意図的に失敗させます。 Irp\_の順序は、\_クエリ\_\_デバイスを停止します (これは、起動中にフィルタードライバーによってエラーが発生し、再調整がキャンセルされます)。 IRP\_\_をキャンセル\_停止\_ドライブ.

    このオプションを使用すると、デバイスのリソースが変更されません。

3.  **PNP 再調整要求の新しいリソースのデバイステスト**このテストは再調整を開始し、デバイスのリソース要件を操作して、実際に新しいリソースがデバイスに割り当てられる可能性を最大化します。 このオプションを使用すると、リソースのないデバイスでも、実際には再調整手順全体を実行できます。
    1.  最初に単純な再調整が開始され、次のような Irp が発生します。
        -   IRP\_\_クエリ\_\_デバイスを停止します (この IRP がすべてのドライバーによって渡されることを前提としています)。 このテストでは、この IRP が失敗したケースが既にカバーされています)。
        -   IRP\_\_クエリ\_リソース\_の要件
        -   IRP\_\_フィルター\_リソース\_要件をフィルター処理します。 この IRP への応答として、フィルタードライバーは、デバイスがリソースを消費しているかどうかに基づいてアクションを実行します。
            -   デバイスにリソース要件がない場合は、フィルターによって偽のリソースが割り当てられます。
            -   デバイスにリソース要件がある場合は、現在の割り当てを変更する確率を最大化するような方法でリソース要件リストを再構築しようとします。 たとえば、デバイスが 00 ~ FF の任意の場所に2バイトのメモリを必要とし、現在は 3A-3B が割り当てられている場合は、新しいリソースの要件 (優先順位) が00-39 または 3C-FF または 3A-3B のように変更されます。 同様に、デバイスリソース要件の一覧に別の要件がある場合は、代替の要件がリストの前に来るように順序を変更します。

    2.  ここで、デバイスは常に再調整手順を完了する必要があります。

        IRP\_\_\_デバイスの停止

        IRP\_、\_デバイス (割り当てられた新しいリソース\_開始します。 偽の要件が作成された場合は、実際のドライバーから新しいリソースをマスクします。)

4.  **PNP 再調整失敗デバイステスト**このテストは再調整を開始しますが、再調整後にフィルタードライバーが開始を取得すると、意図的に失敗します。これにより、突然の削除 IRP の後に削除 IRP が続きます。

    最初に、再調整手順を開始し、リソースを消費しないデバイスのフェイクリソース要件を生成することによって、ドライバーが停止と開始を確実に行うようにします。

    -   IRP\_\_クエリ\_\_デバイスを停止します (この IRP がすべてのドライバーによって渡されることを前提としています)。 このテストでは、この IRP が失敗したケースが既にカバーされています)。
    -   IRP\_\_クエリ\_リソース\_の要件
    -   IRP\_\_フィルター\_リソース\_要件 (実際のリソース要件が null の場合は、フィルターによって仮のリソース要件が割り当てられます。そのため、停止と開始があります)。
    -   IRP\_\_\_デバイスの停止
    -   IRP\_、\_デバイスを起動\_ます (この IRP は、起動中にこの IRP に失敗します。 この操作により、予期しない IRP が削除されます)。
    -   IRP\_\_驚く\_削除
    -   IRP\_\_削除

    再調整テストが完了すると、デバイスがアンインストールされ、再列挙されます。また、フィルタードライバーもスタックから削除されます。

## <a name="device-error-codes"></a>デバイスのエラーコード


デバイスの状態が [OK] でないというエラーメッセージが表示された場合は、デバイスマネージャーでデバイスの状態の詳細を確認してください。 さまざまなデバイスエラーコードの概要については、「[デバイスマネージャーのエラーメッセージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)」を参照してください。

## <a name="debug-installation-failures-using-the-setup-api-logs"></a>セットアップ API ログを使用してインストールエラーをデバッグする


セットアップ API のログ (setupapi.log と setupapi.log) には、このテストで記録されたドライバーのインストールエラーをデバッグするのに役立つ情報が含まれている場合があります。 セットアップ API のログは、テストシステムの% windir%\\inf\\ ディレクトリにあります。

これらのログの詳細度と有用性を向上させるには、再インストールテストを実行する前に、次のレジストリキーを0x2000FFFF に設定します。

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="related-topics"></a>関連トピック


[Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

[デバイスの基本テストを選択して構成する方法](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-select-and-configure-the-device-fundamental-tests)

[デバイスの基本テスト](device-fundamentals-tests.md)

[デバイスの基本テストパラメーター](https://docs.microsoft.com/windows-hardware/drivers)

[指定された WDTF 単純な i/o プラグイン](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)

[コマンドプロンプトから実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

 

 







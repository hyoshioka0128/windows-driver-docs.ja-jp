---
title: カバレッジ テスト (Device Fundamental)
description: デバイスの基本的なカバレッジは、監視して、さまざまな I/O 要求パケット (Irp) を入力するか、指定したデバイスのドライバー スタックのままにするレポートをテストします。
ms.assetid: 950B124B-8B2D-4A54-AFC3-E90BBDD8D1AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08e5da67ea719cc004a8414e224532bc597daa04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343108"
---
# <a name="coverage-tests-device-fundamentals"></a>カバレッジ テスト (Device Fundamental)


デバイスの基本的なカバレッジは、監視して、さまざまな I/O 要求パケット (Irp) を入力するか、指定したデバイスのドライバー スタックのままにするレポートをテストします。 カバレッジのテストからのデータは、ドライバーのテストおよび検証中にカバレッジの弱点を識別できます。

### <a name="span-idcoveragetestsspanspan-idcoveragetestsspancoverage-tests"></a><span id="coverage_tests"></span><span id="COVERAGE_TESTS"></span>カバレッジのテスト

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
<td align="left"><p><span id="Clear_IRP_coverage_data_"></span><span id="clear_irp_coverage_data_"></span><span id="CLEAR_IRP_COVERAGE_DATA_"></span>IRP カバレッジ データのクリア</p></td>
<td align="left"><p>IRP のカバレッジ データを消去します。</p>
<p><strong>バイナリをテストします。</strong>DriverCoverageClearCoverageData.dll</p>
<p><strong>メソッドをテストします。</strong>ClearCoverageData</p>
<p><strong>パラメータ:</strong>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Disable_IRP_coverage_data_collection"></span><span id="disable_irp_coverage_data_collection"></span><span id="DISABLE_IRP_COVERAGE_DATA_COLLECTION"></span>IRP カバレッジ データ コレクションを無効にします。</p></td>
<td align="left"><p>指定されたデバイスの IRP のカバレッジ データ コレクションを無効になります、 <em>DQ</em>パラメーター。</p>
<p><strong>バイナリをテストします。</strong>DriverCoverageDisableSupport.dll</p>
<p><strong>メソッドをテストします。</strong>DisableCoverageDataCollection</p>
<p><strong>パラメータ:</strong></p>
<p><em>DQ</em> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Display_collected_IRP_coverage_data._"></span><span id="display_collected_irp_coverage_data._"></span><span id="DISPLAY_COLLECTED_IRP_COVERAGE_DATA._"></span>収集された IRP のカバレッジ データを表示します。</p></td>
<td align="left"><p>すべてのデバイス用にこのポイントまでに収集された IRP のカバレッジ データを表示します。</p>
<p><strong>バイナリをテストします。</strong>DriverCoverageDisplayCoverage.dll</p>
<p><strong>メソッドをテストします。</strong>DisplayCoverageData</p>
<p><strong>パラメータ:</strong>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Display_IRP_coverage_enabled_devices"></span><span id="display_irp_coverage_enabled_devices"></span><span id="DISPLAY_IRP_COVERAGE_ENABLED_DEVICES"></span>IRP のカバレッジの表示には、デバイスが有効になっています。</p></td>
<td align="left"><p>現在有効になっている IRP カバレッジ データ コレクションにあるデバイスが表示されます。</p>
<p><strong>バイナリをテストします。</strong>DriverCoverageDisplayEnabledDevices.dll</p>
<p><strong>メソッドをテストします。</strong>DisplayEnabledDevices</p>
<p><strong>パラメータ:</strong>なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_IRP_coverage_data_collection"></span><span id="enable_irp_coverage_data_collection"></span><span id="ENABLE_IRP_COVERAGE_DATA_COLLECTION"></span>IRP カバレッジ データ コレクションを有効にします。</p></td>
<td align="left"><p>指定されたデバイスの IRP カバレッジ データ コレクションを有効に、 <em>DQ</em>パラメーター。</p>
<p><strong>バイナリをテストします。</strong>DriverCoverageEnableSupport.dll</p>
<p><strong>メソッドをテストします。</strong>EnableCoverageDataCollection</p>
<p><strong>パラメータ:</strong>なし</p>
<p><em>DQ</em> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idaboutthecoveragetestsspanspan-idaboutthecoveragetestsspanspan-idaboutthecoveragetestsspanabout-the-coverage-tests"></a><span id="About_the_Coverage_tests"></span><span id="about_the_coverage_tests"></span><span id="ABOUT_THE_COVERAGE_TESTS"></span>カバレッジのテストについて

デバイス基本カバレッジのテストは、以前は、WDK でスタンドアロン ツールとして使用するが、ドライバーのカバレッジ Toolkit に基づいています。 カバレッジのテストを実装する方法については、次を参照してください。[ドライバー カバレッジ Toolkit](driver-coverage-toolkit.md)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供されている WDTF シンプル I/O プラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 







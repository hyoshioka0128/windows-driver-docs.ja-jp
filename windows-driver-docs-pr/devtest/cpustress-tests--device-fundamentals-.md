---
title: CPUStress テスト (Device Fundamental)
description: CpuStress テストでは、別のプロセッサ使用率のレベルを持つデバイス I/O のテストを実行します。
ms.assetid: E546C3A3-89E6-450B-90D3-4F349A3EC495
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5522ecb85b757e545c62c0b76b84da23104d1d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538292"
---
# <a name="cpustress-tests-device-fundamentals"></a>CPUStress テスト (Device Fundamental)


CpuStress テストでは、別のプロセッサ使用率のレベルを持つデバイス I/O のテストを実行します。

## <a name="span-idcpustresstestsspanspan-idcpustresstestsspancpustress"></a><span id="cpu_stress_tests"></span><span id="CPU_STRESS_TESTS"></span>CpuStress


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
<td align="left"><p><span id="Device_I_O_with_alternating_processor_utilization_levels"></span><span id="device_i_o_with_alternating_processor_utilization_levels"></span><span id="DEVICE_I_O_WITH_ALTERNATING_PROCESSOR_UTILIZATION_LEVELS"></span>デバイス I/O がプロセッサ使用率のレベルを交互に使用</p></td>
<td align="left"><p>このテストでは、高 (HPU) と (LPU) プロセッサ使用率のレベルが低い交互中にデバイス I/O をテストします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>メソッドをテストします。</strong>Device_IO_With_Varying_ProcUtil</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>PingPongPeriod</em></p>
<p><em>HPU</em></p>
<p><em>LPU</em></p>
<p><em>TestCycles</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Device_I_O_with_a_fixed_processor_utilization_level"></span><span id="device_i_o_with_a_fixed_processor_utilization_level"></span><span id="DEVICE_I_O_WITH_A_FIXED_PROCESSOR_UTILIZATION_LEVEL"></span>固定のプロセッサ使用率のレベルを持つデバイス I/O</p></td>
<td align="left"><p>このテストでは、デバイス I/O のプロセッサ使用率 (PU) レベルの固定の比率に設定をテストします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>メソッドをテストします。</strong>Device_IO_With_Fixed_ProcUtil</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Device_PNP_with_a_fixed_processor_utilization_level"></span><span id="device_pnp_with_a_fixed_processor_utilization_level"></span><span id="DEVICE_PNP_WITH_A_FIXED_PROCESSOR_UTILIZATION_LEVEL"></span>固定のプロセッサ使用率のレベルを持つデバイス PNP</p></td>
<td align="left"><p>このテストでは、デバイスの PNP テスト プロセッサ使用率 (PU) レベルの固定の比率に設定します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>メソッドをテストします。</strong>Device_PNP_With_Fixed_ProcUtil</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_fixed_processor_utilization_"></span><span id="sleep_with_fixed_processor_utilization_"></span><span id="SLEEP_WITH_FIXED_PROCESSOR_UTILIZATION_"></span>固定のプロセッサ使用率のスリープ状態します。</p></td>
<td align="left"><p>このテストでは、さまざまなスリープ状態を使用してシステムをサイクル プロセッサ使用率のレベルが固定の比率に設定します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>メソッドをテストします。</strong>Sleep_With_Fixed_ProcUtil</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio を使用して実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[デバイスの基本テスト](device-fundamentals-tests.md)

[デバイス基礎テスト パラメーター](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[単純な I/O の WDTF プラグインを提供](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 







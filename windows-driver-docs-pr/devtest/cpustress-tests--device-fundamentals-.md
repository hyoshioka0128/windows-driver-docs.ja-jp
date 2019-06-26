---
title: CPUStress テスト (Device Fundamental)
description: CpuStress テストでは、別のプロセッサ使用率のレベルを持つデバイス I/O のテストを実行します。
ms.assetid: E546C3A3-89E6-450B-90D3-4F349A3EC495
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 542e035b28811bdaf848ea9d11e72f666eaf7c7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360380"
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
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
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
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Device_PNP_with_a_fixed_processor_utilization_level"></span><span id="device_pnp_with_a_fixed_processor_utilization_level"></span><span id="DEVICE_PNP_WITH_A_FIXED_PROCESSOR_UTILIZATION_LEVEL"></span>固定のプロセッサ使用率のレベルを持つデバイス PNP</p></td>
<td align="left"><p>このテストでは、デバイスの PNP テスト プロセッサ使用率 (PU) レベルの固定の比率に設定します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>メソッドをテストします。</strong>Device_PNP_With_Fixed_ProcUtil</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_fixed_processor_utilization_"></span><span id="sleep_with_fixed_processor_utilization_"></span><span id="SLEEP_WITH_FIXED_PROCESSOR_UTILIZATION_"></span>固定のプロセッサ使用率のスリープ状態します。</p></td>
<td align="left"><p>このテストでは、さまざまなスリープ状態を使用してシステムをサイクル プロセッサ使用率のレベルが固定の比率に設定します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_ProcUtil_PingPong_With_IO.wsc</p>
<p><strong>メソッドをテストします。</strong>Sleep_With_Fixed_ProcUtil</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>TestCycles</em></p>
<p><em>PU</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

[テストを選択し、デバイスの基本を構成する方法](https://docs.microsoft.com/windows-hardware/drivers)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://docs.microsoft.com/windows-hardware/drivers)

[提供されている WDTF シンプル I/O プラグイン](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

 

 







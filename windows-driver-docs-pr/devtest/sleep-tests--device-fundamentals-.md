---
title: スリープ テスト (Device Fundamental)
description: デバイス基礎スリープ テスト実行 I/O と、指定したデバイス、PnP 操作前に、と後に、またはシステムのスリープ中に状態遷移します。
ms.assetid: 38B65078-B436-4C24-B973-032702DB9CBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9b999026826800dc9fce6e6294ccc20c53c345e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571519"
---
# <a name="sleep-tests-device-fundamentals"></a>スリープ テスト (Device Fundamental)


デバイス基礎スリープ テスト実行 I/O と、指定したデバイス、PnP 操作前に、と後に、またはシステムのスリープ中に状態遷移します。 スリープのテストでは、テスト対象のデバイスがすべてのサポートされるスリープ状態を循環できるシステムにできることを確認します。 さらに、単純な I/O ストレス テストを使用してこれらの状態変更した後、デバイスがまだ機能があるようになります。

## <a name="sleep-tests"></a>スリープのテスト


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
<td align="left"><p><span id="Critical_Sleep_with_I_O_before_and_after"></span><span id="critical_sleep_with_i_o_before_and_after"></span><span id="CRITICAL_SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>前に、と後の I/O でクリティカルなスリープ</p></td>
<td align="left"><p>このテストでは、システムにクリティカルなスリープ状態の遷移を実行し、各スリープ状態のサイクルの前後の前にデバイスでは、I/O を実行します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Critical_Sleep_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>Critical_Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Critical_Sleep_with_I_O_during"></span><span id="critical_sleep_with_i_o_during"></span><span id="CRITICAL_SLEEP_WITH_I_O_DURING"></span>クリティカル スリープ中に i/o</p></td>
<td align="left"><p>このテストでは、システムにクリティカルなスリープ状態の遷移を実行し、デバイスで I/O を実行します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Critical_Sleep_With_IO_During.wsc</p>
<p><strong>メソッドをテストします。</strong>Critical_Sleep_With_IO_During</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_and_PNP__disable_and_enable__with_I_O_Before_and_After"></span><span id="sleep_and_pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="SLEEP_AND_PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>スリープと PNP (無効および有効にする) と後の I/O の前に</p></td>
<td align="left"><p>このテストでは、さまざまなスリープ状態を使用してシステムをサイクルし、スリープ状態、各サイクルの前後に I/O と基本的な PnP (無効/有効にする) デバイスでを実行します。</p>
<p>詳細については、次を参照してください。<a href="#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test" data-raw-source="[About the Sleep and PNP disable and enable with IO Before and After test](#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test)">について Sleep and PNP と無効にし、テストの前後に IO の前に有効にする</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Sleep_PNP_DisableEnable_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>Sleep_PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_I_O_Before_and_After"></span><span id="sleep_with_i_o_before_and_after"></span><span id="SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>前に、と後の I/O でスリープします。</p></td>
<td align="left"><p>このテストでは、サイクルのさまざまなスリープ状態により、システム、スリープ状態、各サイクルの前後には、デバイスの I/O を実行します。</p>
<p>詳細については、次を参照してください。<a href="#about-the-sleep-with-io-before-and-after-test" data-raw-source="[About the Sleep with IO Before And After test](#about-the-sleep-with-io-before-and-after-test)">について、スリープ状態で IO の前と後にテスト</a>します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Sleep_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>Sleep_With_Io_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_with_I_O_during"></span><span id="sleep_with_i_o_during"></span><span id="SLEEP_WITH_I_O_DURING"></span>スリープ中に i/o</p></td>
<td align="left"><p>このテストでは、サイクルのさまざまなスリープ状態により、システム、デバイスの I/O を実行します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Sleep_With_IO_During.wsc</p>
<p><strong>メソッドをテストします。</strong>Sleep_With_IO_During</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test"></a>スリープと PNP について無効にし、テストの前後に IO の前に有効にします。


このテストは、次を行います。

1.  テスト デバイスとその子孫が、デバイスの問題のコードのレポートでされていないことを確認します。
2.  テスト デバイスとその子孫 WDTF 単純な I/O プラグインを使用して I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
3.  最初のサポートされるスリープ状態にテスト システムを送信し、しばらくスリープ状態からシステムを再開します。
4.  テスト デバイスとその子孫が、デバイスの問題のコードのレポートでされていないことを確認します。
5.  テスト デバイスとその子孫 WDTF 単純な I/O プラグインを使用して I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
6.  テスト デバイスの場合は、無効になっていますテストは無効にし、WDTF PnP アクション インターフェイスを使用して、テスト デバイスを参照してください[ **IWDTFPNPAction2::DisableDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh451068)と[  **。IWDTFPNPAction2::EnableDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh451082)方法の詳細について。
7.  テスト デバイスとその子孫が、デバイスの問題のコードのレポートでされていないことを確認します。
8.  テスト デバイスとその子孫 WDTF 単純な I/O プラグインを使用して I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
9.  各繰り返し手順 3 ~ 8 には、テスト システムのスリープ状態がサポートされています。
10. 繰り返し何度も 1 ~ 9 をステップします。

## <a name="about-the-sleep-with-io-before-and-after-test"></a>IO の前に、と後にテストをスリープ状態について


このテストは、次を行います。

1.  デバイスの問題のコードをレポート作成システム上のデバイスがないことを確認します。
2.  WDTF 単純な I/O プラグインを使用して、システム上のすべてのデバイスで I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
3.  最初のサポートされるスリープ状態にテスト システムを送信し、しばらくスリープ状態からシステムを再開します。
4.  デバイスの問題のコードをレポート作成システム上のデバイスがないことを確認します。
5.  WDTF 単純な I/O プラグインを使用して、システム上のすべてのデバイスで I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
6.  テスト システムの場合は、各サポートされるスリープ状態には、手順 3. ~ 5. を繰り返します。
7.  数回の手順 1. ~ 6. を繰り返します。

## <a name="related-topics"></a>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供されている WDTF シンプル I/O プラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 







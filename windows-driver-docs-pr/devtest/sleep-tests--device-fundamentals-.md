---
title: スリープテスト (デバイスの基本)
description: デバイスの基本スリープテストでは、指定されたデバイス、前後、またはシステムスリープ状態遷移中に、i/o と PnP 操作を実行します。
ms.assetid: 38B65078-B436-4C24-B973-032702DB9CBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d7c25bfc511844ddc0837d3870a2356396241d2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839326"
---
# <a name="sleep-tests-device-fundamentals"></a>スリープテスト (デバイスの基本)


デバイスの基本スリープテストでは、指定されたデバイス、前後、またはシステムスリープ状態遷移中に、i/o と PnP 操作を実行します。 スリープテストでは、テスト対象のデバイスが、サポートされているすべてのスリープ状態を使用してシステムを循環することを許可します。 また、単純な i/o ストレステストによってこれらの状態が変更された後も、デバイスが引き続き機能することを保証します。

## <a name="sleep-tests"></a>スリープテスト


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
<td align="left"><p><span id="Critical_Sleep_with_I_O_before_and_after"></span><span id="critical_sleep_with_i_o_before_and_after"></span><span id="CRITICAL_SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>I/o の前後の重大なスリープ</p></td>
<td align="left"><p>このテストは、システムに対して重大なスリープ状態遷移を実行し、各スリープ状態サイクルの前後にデバイスで i/o を実行します。</p>
<p><strong>テストバイナリ:</strong>Devfund_Critical_Sleep_With_IO_BeforeAndAfter</p>
<p><strong>テストメソッド:</strong>Critical_Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Critical_Sleep_with_I_O_during"></span><span id="critical_sleep_with_i_o_during"></span><span id="CRITICAL_SLEEP_WITH_I_O_DURING"></span>重大なスリープ状態</p></td>
<td align="left"><p>このテストは、システムでの重大なスリープ状態遷移を実行し、デバイスで i/o を実行します。</p>
<p><strong>テストバイナリ:</strong>Devfund_Critical_Sleep_With_IO_During</p>
<p><strong>テストメソッド:</strong>Critical_Sleep_With_IO_During</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_and_PNP__disable_and_enable__with_I_O_Before_and_After"></span><span id="sleep_and_pnp__disable_and_enable__with_i_o_before_and_after"></span><span id="SLEEP_AND_PNP__DISABLE_AND_ENABLE__WITH_I_O_BEFORE_AND_AFTER"></span>スリープと PNP (無効化および有効化) と i/o の前後</p></td>
<td align="left"><p>このテストでは、さまざまなスリープ状態を通じてシステムをサイクル化し、各スリープ状態サイクルの前後にデバイスで i/o と基本的な PnP (無効化/有効化) を実行します。</p>
<p>詳細については、「<a href="#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test" data-raw-source="[About the Sleep and PNP disable and enable with IO Before and After test](#about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test)">テストの前後のスリープと PNP の無効化と有効化</a>」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_Sleep_PNP_DisableEnable_With_IO_BeforeAndAfter</p>
<p><strong>テストメソッド:</strong>Sleep_PNP_DisableEnable_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Sleep_with_I_O_Before_and_After"></span><span id="sleep_with_i_o_before_and_after"></span><span id="SLEEP_WITH_I_O_BEFORE_AND_AFTER"></span>前後の i/o でスリープする</p></td>
<td align="left"><p>このテストでは、さまざまなスリープ状態を通じてシステムをサイクルし、各スリープ状態サイクルの前後にデバイスで i/o を実行します。</p>
<p>詳細については、「<a href="#about-the-sleep-with-io-before-and-after-test" data-raw-source="[About the Sleep with IO Before And After test](#about-the-sleep-with-io-before-and-after-test)">テストの前後に IO を使用する</a>」を参照してください。</p>
<p><strong>テストバイナリ:</strong>Devfund_Sleep_With_IO_BeforeAndAfter</p>
<p><strong>テストメソッド:</strong>Sleep_With_Io_Before_And_After</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Sleep_with_I_O_during"></span><span id="sleep_with_i_o_during"></span><span id="SLEEP_WITH_I_O_DURING"></span>I/o を使用したスリープ状態</p></td>
<td align="left"><p>このテストでは、さまざまなスリープ状態を使用してシステムをサイクルし、デバイスで i/o を実行します。</p>
<p><strong>テストバイナリ:</strong>Devfund_Sleep_With_IO_During</p>
<p><strong>テストメソッド:</strong>Sleep_With_IO_During</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ResumeDelay</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-sleep-and-pnp-disable-and-enable-with-io-before-and-after-test"></a>スリープと PNP についてテストの前後に IO を無効化および有効化する


このテストは次のことを行います。

1.  テストデバイスとその子孫がデバイスの問題コードを報告していないことを確認します。
2.  WDTF Simple i/o プラグインを使用して、テストデバイスとその子孫の i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
3.  テストシステムを最初にサポートされているスリープ状態に送信し、しばらくしてからシステムをスリープ状態から再開します。
4.  テストデバイスとその子孫がデバイスの問題コードを報告していないことを確認します。
5.  WDTF Simple i/o プラグインを使用して、テストデバイスとその子孫の i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
6.  テストデバイスが無効になっている場合、テストでは WDTF PnP action インターフェイスを使用してテストデバイスを無効にし、有効にします。詳細については、「 [**IWDTFPNPAction2::D isableDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-disabledevice) 」と「 [**IWDTFPNPAction2:: enabledevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfpnpaction/nf-wdtfpnpaction-iwdtfpnpaction2-enabledevice)メソッド」を参照してください。
7.  テストデバイスとその子孫がデバイスの問題コードを報告していないことを確認します。
8.  WDTF Simple i/o プラグインを使用して、テストデバイスとその子孫の i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
9.  テストシステムのサポートされている各スリープ状態について、手順3-8 を繰り返します。
10. 手順1-9 を何度か繰り返します。

## <a name="about-the-sleep-with-io-before-and-after-test"></a>テストの前後の IO に関するスリープについて


このテストは次のことを行います。

1.  システムレポートデバイスの問題コードにデバイスがないことを確認します。
2.  WDTF Simple i/o プラグインを使用して、システム上のすべてのデバイスで i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
3.  テストシステムを最初にサポートされているスリープ状態に送信し、しばらくしてからシステムをスリープ状態から再開します。
4.  システムレポートデバイスの問題コードにデバイスがないことを確認します。
5.  WDTF Simple i/o プラグインを使用して、システム上のすべてのデバイスで i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
6.  テストシステムのサポートされている各スリープ状態について、手順 3-5 を繰り返します。
7.  手順 1-6 を何度か繰り返します。

## <a name="related-topics"></a>関連トピック


[Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

[デバイスの基本テストを選択して構成する方法](https://docs.microsoft.com/windows-hardware/drivers)

[デバイスの基本テスト](device-fundamentals-tests.md)

[デバイスの基本テストパラメーター](https://docs.microsoft.com/windows-hardware/drivers)

[指定された WDTF 単純な i/o プラグイン](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)

[コマンドプロンプトから実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

 

 







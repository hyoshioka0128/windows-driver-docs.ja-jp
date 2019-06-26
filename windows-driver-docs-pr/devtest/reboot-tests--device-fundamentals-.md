---
title: 再起動テスト (Device Fundamental)
description: デバイスの基礎の再起動のテストは前に、と後に、またはシステムの再起動中に、指定したデバイスの I/O を実行します。
ms.assetid: 71EBEC60-C99F-412D-8FC5-2DD9209CC92D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38b7e50445b97e035132bb6fbfdf32dc23b85076
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375874"
---
# <a name="reboot-tests-device-fundamentals"></a>再起動テスト (Device Fundamental)


デバイスの基礎の再起動のテストは前に、と後に、またはシステムの再起動中に、指定したデバイスの I/O を実行します。

## <a name="span-idreboottestsspanspan-idreboottestsspanreboot-tests"></a><span id="reboot_tests"></span><span id="REBOOT_TESTS"></span>テストを再起動します。


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
<td align="left"><p><span id="Critical_Reboot_Restart_with_I_O_before_and_after"></span><span id="critical_reboot_restart_with_i_o_before_and_after"></span><span id="CRITICAL_REBOOT_RESTART_WITH_I_O_BEFORE_AND_AFTER"></span>重要な再起動して再起動 I/O 前に、と後</p></td>
<td align="left"><p>このテストでは、重要なシステム再起動の前後に、I/O がデバイスで実行されます。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Critical_RebootRestart_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>Critical_Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Critical_Reboot_Restart_with_I_O_during"></span><span id="critical_reboot_restart_with_i_o_during"></span><span id="CRITICAL_REBOOT_RESTART_WITH_I_O_DURING"></span>重要な再起動の再起動中に i/o</p></td>
<td align="left"><p>このテストは、I/O の実行中の重要な再起動を開始、および再起動の後にもう一度 SimpleI/O を実行するデバイスで単純な I/O を開始します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Critical_RebootRestart_With_IO_During.wsc</p>
<p><strong>メソッドをテストします。</strong>Critical_Reboot_Restart_With_IO_During</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Reboot_Restart_with_I_O_before_and_after"></span><span id="reboot_restart_with_i_o_before_and_after"></span><span id="REBOOT_RESTART_WITH_I_O_BEFORE_AND_AFTER"></span>I/O で再起動の前に、と後の再起動します。</p></td>
<td align="left"><p>このテストでは前に、と、システムの再起動後に、I/O がデバイスで実行されます。</p>
<p><strong>バイナリをテストします。</strong>Devfund_RebootRestart_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>Reboot_Restart_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Reboot_restart_with_I_O_during"></span><span id="reboot_restart_with_i_o_during"></span><span id="REBOOT_RESTART_WITH_I_O_DURING"></span>再起動中に I/O と再起動します。</p></td>
<td align="left"><p>このテストは、I/O の実行中の再起動を開始、および再起動の後にもう一度 SimpleI/O を実行するデバイスで単純な I/O を開始します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_RebootRestart_With_IO_During.wsc</p>
<p><strong>メソッドをテストします。</strong>Reboot_Restart_With_IO_During</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p></td>
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

 

 







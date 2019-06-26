---
title: I/O テスト (Device Fundamental)
description: デバイスの基本 I/O テストでは、指定したデバイスの基本的な I/O テストを実行します。
ms.assetid: 4FF125BE-846A-4A93-9B4F-C6BC469EA0AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb8dd3ef53d503193938b8cc0e66d6e416a10d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356511"
---
# <a name="io-tests-device-fundamentals"></a>I/O テスト (Device Fundamental)


デバイスの基本 I/O テストでは、指定したデバイスの基本的な I/O テストを実行します。

## <a name="span-idiotestsspanspan-idiotestsspanio-tests"></a><span id="io_tests"></span><span id="IO_TESTS"></span>I/O のテスト


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
<td align="left"><p><span id="Device_I_O_"></span><span id="device_i_o_"></span><span id="DEVICE_I_O_"></span>デバイス I/O</p></td>
<td align="left"><p>このテストでは、基本的な I/O のテスト デバイスで実行します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Device_IO.wsc</p>
<p><strong>メソッドをテストします。</strong>DeviceIO</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>IOPeriod</em></p>
<p><em>IOType</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Simple_I_O_stress_test_with_I_O_process_termination"></span><span id="simple_i_o_stress_test_with_i_o_process_termination"></span><span id="SIMPLE_I_O_STRESS_TEST_WITH_I_O_PROCESS_TERMINATION"></span>プロセス終了の I/O での単純な I/O ストレス テスト</p></td>
<td align="left"><p>このテストでは、別のプロセスでのデバイスでの単純な I/O テストを実行し、指定した I/O の期間およびテスト サイクルの後に I/O 処理を終了します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_SimpleIoStress_TermIoProc.wsc</p>
<p><strong>メソッドをテストします。</strong>SimpleIOStress_TermIoProc</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>IOPeriod</em></p></td>
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

 

 







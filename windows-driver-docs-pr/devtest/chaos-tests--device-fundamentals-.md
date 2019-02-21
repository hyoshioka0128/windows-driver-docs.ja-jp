---
title: CHAOS テスト (Device Fundamental)
description: (同時実行ハードウェアおよびオペレーティング システム) の混乱のテストがテスト PnP ドライバーさまざまなデバイス ドライバーのファジー テストを実行し、システムの電源が同時にテストします。
ms.assetid: FA0D73DC-B0B8-4CA7-8DDC-A2C3EC106C3F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ba7b831802cf9ffe7b76bc5b29526a0c10cbf23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549051"
---
# <a name="chaos-tests-device-fundamentals"></a>CHAOS テスト (Device Fundamental)


(同時実行ハードウェアおよびオペレーティング システム) の混乱のテストがテスト PnP ドライバーさまざまなデバイス ドライバーのファジー テストを実行し、システムの電源が同時にテストします。

### <a name="span-idcoveragetestsspanspan-idcoveragetestsspanchaos-tests"></a><span id="coverage_tests"></span><span id="COVERAGE_TESTS"></span>混乱のテスト

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
<p>PnP ドライバー テストでは、EDT フィルター ドライバーを使用して、ターゲット デバイス スタックを IRP_MN_CANCEL_REMOVE_DEVICE を送信します。</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Run_CHAOS_Test"></span><span id="run_chaos_test"></span><span id="RUN_CHAOS_TEST"></span>混乱のテストを実行します。</p></td>
<td align="left"><p>実行テスト PnP ドライバー パッケージとファジーすべてサポートされているシステム電源の状態により、システムを循環しながら、並列でテストします。 PnP ドライバー テストでは、PnP 操作の実行中にターゲット デバイス スタックを I/O 要求を送信します。</p>
<p>このテストのテスト システムとの間、サポートされている状態 (S1、S2、S3、S4、接続済みのすべてのサイクル中には、並列でテスト デバイスに対して (有効/無効に、再調整、削除/再起動、突然の削除、および削除の差分) PnP テストを実行し、ドライバーのファジー テスト同時に、スタンバイ)。 このテストの目的は、PNP、I/O、および電源の同時実行シナリオをテストし、クラッシュの検索があるか、プロセスにハングします。</p>
<p><strong>バイナリをテストします。</strong>Devfund_ChaosTest.dll</p>
<p><strong>メソッドをテストします。</strong>RunCHAOSTest</p>
<p><strong>パラメータ:</strong></p>
<p><em>DQ</em> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>TestPeriod</em> - (分) でテストを実行する時間を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio を使用して実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[デバイスの基本テスト](device-fundamentals-tests.md)

[デバイス基礎テスト パラメーター](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[PwrTest](pwrtest.md)

[侵入テスト (デバイスの基本)](penetration-tests--device-fundamentals-.md)

[PnP テスト (デバイスの基本)](pnp-tests--device-fundamentals-.md)

 

 







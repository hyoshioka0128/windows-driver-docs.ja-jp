---
title: Driver Install テスト (Device Fundamental)
description: ドライバーインストールテストカテゴリには、ドライバーをアンインストールして、インストール機能をテストするために何度か再インストールするテストが含まれています。
ms.assetid: 3FC00D4B-6520-45F1-805C-A5F8B6AACAC8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 025f298797753685bc541cd573239bfa9498e3f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840275"
---
# <a name="driver-install-tests-device-fundamentals"></a>Driver Install テスト (Device Fundamental)


ドライバーインストールテストカテゴリには、ドライバーをアンインストールして、インストール機能をテストするために何度か再インストールするテストが含まれています。 テストでは、再インストールのたびに、ドライバーとデバイスに対して i/o テストが開始されます。 このテストは、デバイスドライバーまたはデバイスをインストールして再インストールする必要があるエンドユーザーの全体的なエクスペリエンスを向上させるように設計されています。

## <a name="span-iddriverinstall_testsspanspan-iddriverinstall_testsspandriverinstall-tests"></a><span id="driverinstall_tests"></span><span id="DRIVERINSTALL_TESTS"></span>DriverInstall テスト


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
<td align="left"><p><span id="Reinstall_with_IO_Before_and_After"></span><span id="reinstall_with_io_before_and_after"></span><span id="REINSTALL_WITH_IO_BEFORE_AND_AFTER"></span>IO の前後の再インストール</p></td>
<td align="left"><p>このテストでは、選択したデバイスのドライバーをアンインストールして再インストールし、デバイスで i/o テストを実行します。</p>
<p><strong>テストバイナリ:</strong>Devfund_Reinstall_With_IO_BeforeAndAfter</p>
<p><strong>テストメソッド:</strong>Reinstall_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> - 「<a href="https://docs.microsoft.com/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](https://docs.microsoft.com/windows-hardware/drivers)">デバイスの基本テストパラメーター</a> 」を参照</p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idabout_the_reinstall_with_i_o_before_and_after_testspanspan-idabout_the_reinstall_with_i_o_before_and_after_testspanspan-idabout_the_reinstall_with_i_o_before_and_after_testspanabout-the-reinstall-with-io-before-and-after-test"></a><span id="About_the_ReInstall_with_I_O_Before_and_After_test"></span><span id="about_the_reinstall_with_i_o_before_and_after_test"></span><span id="ABOUT_THE_REINSTALL_WITH_I_O_BEFORE_AND_AFTER_TEST"></span>テストの前後の i/o を使用した再インストールについて


このテストは次のことを行います。

1.  テストデバイスとその子孫がデバイスの問題コードを報告していないことを確認します。
2.  WDTF Simple i/o プラグインを使用して、テストデバイスとその子孫の i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
3.  [**IWDTFDriverSetupAction2:: UpdateDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-updatedriver)メソッドを使用して、テストデバイスに元のドライバーを再インストールします。
4.  テストデバイスとその子孫がデバイスの問題コードを報告していないことを確認します。
5.  WDTF Simple i/o プラグインを使用して、テストデバイスとその子孫の i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
6.  ステップ \#3 で再起動が必要な場合は、システムを再起動します。
7.  [**IWDTFDriverSetupAction2:: UnInstallDriverPermanently**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-uninstalldriverpermanently)メソッドを使用して、テストデバイスに NULL ドライバーをインストールします。再起動が必要な場合は、システムが再起動されます。
8.  [**IWDTFDriverSetupAction2:: UpdateDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nf-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2-updatedriver)メソッドを使用して、テスト対象のデバイスに元のドライバーを再インストールします。
9.  テストデバイスとその子孫がデバイスの問題コードを報告していないことを確認します。
10. WDTF Simple i/o プラグインを使用して、テストデバイスとその子孫の i/o をテストします。 詳細については、「 [WDTF Simple i/o プラグインの提供](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)」を参照してください。
11. 手順 1-10 を何度か繰り返します。

### <a name="span-iddebug_installation_failures_using_the_setup_api_logsspanspan-iddebug_installation_failures_using_the_setup_api_logsspanspan-iddebug_installation_failures_using_the_setup_api_logsspandebug-installation-failures-using-the-setup-api-logs"></a><span id="Debug_installation_failures_using_the_Setup_API_logs"></span><span id="debug_installation_failures_using_the_setup_api_logs"></span><span id="DEBUG_INSTALLATION_FAILURES_USING_THE_SETUP_API_LOGS"></span>セットアップ API ログを使用してインストールエラーをデバッグする

セットアップ API のログ (setupapi.log と setupapi.log) には、このテストで記録されたドライバーのインストールエラーをデバッグするのに役立つ情報が含まれています。 セットアップ API のログは、テストシステムの% windir%\\inf\\ ディレクトリにあります。

これらのログの詳細度と有用性を向上させるには、再インストールテストを実行する前に、次のレジストリキーを0x2000FFFF に設定します。

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

[デバイスの基本テストを選択して構成する方法](https://docs.microsoft.com/windows-hardware/drivers)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://docs.microsoft.com/windows-hardware/drivers)

[提供されている WDTF シンプル I/O プラグイン](https://docs.microsoft.com/windows-hardware/drivers/wdtf/provided-wdtf-simpleio-plug-ins)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)

 

 







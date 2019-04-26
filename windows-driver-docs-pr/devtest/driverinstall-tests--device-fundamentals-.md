---
title: Driver Install テスト (Device Fundamental)
description: 機能をインストールするドライバーのインストール テスト カテゴリには、テストするテスト アンインストールしてドライバーを何度も再インストールにはが含まれています。
ms.assetid: 3FC00D4B-6520-45F1-805C-A5F8B6AACAC8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eedcb75a749a1e843b34c806be59cf0a49414112
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344848"
---
# <a name="driver-install-tests-device-fundamentals"></a>Driver Install テスト (Device Fundamental)


機能をインストールするドライバーのインストール テスト カテゴリには、テストするテスト アンインストールしてドライバーを何度も再インストールにはが含まれています。 テストでは、I/O が各を再インストールした後、ドライバーとデバイスに対してテストを開始します。 テストは、インストールし、デバイス ドライバーまたはデバイスを再インストールする必要があるエンドユーザーの全体的なエクスペリエンスを向上させるために設計されています。

## <a name="span-iddriverinstalltestsspanspan-iddriverinstalltestsspandriverinstall-tests"></a><span id="driverinstall_tests"></span><span id="DRIVERINSTALL_TESTS"></span>DriverInstall テスト


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
<td align="left"><p><span id="Reinstall_with_IO_Before_and_After"></span><span id="reinstall_with_io_before_and_after"></span><span id="REINSTALL_WITH_IO_BEFORE_AND_AFTER"></span>前後に IO を再インストールします。</p></td>
<td align="left"><p>このテストは、アンインストールし、選択したデバイスのドライバーを再インストールし、I/O デバイスでテストを実行します。</p>
<p><strong>バイナリをテストします。</strong>Devfund_Reinstall_With_IO_BeforeAndAfter.wsc</p>
<p><strong>メソッドをテストします。</strong>Reinstall_With_IO_Before_And_After</p>
<p><strong>パラメーター:</strong> -を参照してください<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">デバイス基礎テスト パラメーター</a></p>
<p><em>DQ</em></p>
<p><em>IOPeriod</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idaboutthereinstallwithiobeforeandaftertestspanspan-idaboutthereinstallwithiobeforeandaftertestspanspan-idaboutthereinstallwithiobeforeandaftertestspanabout-the-reinstall-with-io-before-and-after-test"></a><span id="About_the_ReInstall_with_I_O_Before_and_After_test"></span><span id="about_the_reinstall_with_i_o_before_and_after_test"></span><span id="ABOUT_THE_REINSTALL_WITH_I_O_BEFORE_AND_AFTER_TEST"></span>テストの前後で I/O の前に再インストールについて


このテストは、次を行います。

1.  テスト デバイスとその子孫が、デバイスの問題のコードのレポートでされていないことを確認します。
2.  テスト デバイスとその子孫 WDTF 単純な I/O プラグインを使用して I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
3.  テスト デバイスの使用を元のドライバを再インストール[ **IWDTFDriverSetupAction2::UpdateDriver** ](https://msdn.microsoft.com/library/windows/hardware/hh450945)メソッド。
4.  テスト デバイスとその子孫が、デバイスの問題のコードのレポートでされていないことを確認します。
5.  テスト デバイスとその子孫 WDTF 単純な I/O プラグインを使用して I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
6.  場合に、システムを再起動する手順\#3 には、再起動が必要です。
7.  NULL ドライバーをインストール、テスト デバイスを使用して[ **IWDTFDriverSetupAction2::UnInstallDriverPermanently** ](https://msdn.microsoft.com/library/windows/hardware/hh450941)メソッドは、再起動が必要な場合に、システムを再起動します。
8.  使用してテスト下のデバイスを元のドライバを再インストール[ **IWDTFDriverSetupAction2::UpdateDriver** ](https://msdn.microsoft.com/library/windows/hardware/hh450945)メソッド。
9.  テスト デバイスとその子孫が、デバイスの問題のコードのレポートでされていないことを確認します。
10. テスト デバイスとその子孫 WDTF 単純な I/O プラグインを使用して I/O をテストします。 参照してください[WDTF の単純な I/O を提供するプラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)詳細についてはします。
11. 繰り返し何度も 1 ~ 10 をステップします。

### <a name="span-iddebuginstallationfailuresusingthesetupapilogsspanspan-iddebuginstallationfailuresusingthesetupapilogsspanspan-iddebuginstallationfailuresusingthesetupapilogsspandebug-installation-failures-using-the-setup-api-logs"></a><span id="Debug_installation_failures_using_the_Setup_API_logs"></span><span id="debug_installation_failures_using_the_setup_api_logs"></span><span id="DEBUG_INSTALLATION_FAILURES_USING_THE_SETUP_API_LOGS"></span>API のセットアップ ログを使用して、インストール エラーをデバッグします。

API のセットアップのログ (setupapi.app.log および setupapi.dev.log) には、このテストで記録されたドライバーのインストール エラーのデバッグに役立つ情報が含まれます。 API のセットアップ ログは %windir% あります\\inf\\テスト システムのディレクトリ。

詳細およびこれらのログの潜在的な有用性を向上させるのには、テストの再インストールを実行する前に次のレジストリ キーを 0x2000FFFF に設定します。

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\LogLevel
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[テストを選択し、デバイスの基本を構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[Device Fundamental のテスト](device-fundamentals-tests.md)

[Device Fundamental テストのパラメーター](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供されている WDTF シンプル I/O プラグイン](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[コマンド プロンプトから実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 







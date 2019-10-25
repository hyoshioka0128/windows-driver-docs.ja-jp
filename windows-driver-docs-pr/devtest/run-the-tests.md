---
title: テストの実行
description: Windows ドライバーのデータドリブン SysFund テスト用のテストおよび構成ファイルの説明
keywords:
- Sysfund テスト
- データドリブンテスト
- SDEL クエリ
ms.date: 11/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab393dd0e4794015c8a96535b2d3b9d4461e6eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840045"
---
# <a name="run-the-tests"></a>テストの実行
## <a name="description-of-the-tests-and-configuration-file"></a>テストと構成ファイルの説明
データ主導型の SysFund テストは、\<解凍された EWDK ルート > Kits\10\Testing\Tests\Additional Files\Windows Testrix64/devfundで見つかります。  データドリブンテストスイートは、次のファイルで構成されています。

- XML 構成ファイル WDTFTest .xml を使用する5つのテスト DLL。

  *   Sysfund_Device_IO_DataDriven
  *   Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven
  *   Sysfund_PNP_RemoveAndRestartDevice_DataDriven
  *   Sysfund_RebootRestart_With_IO_During_DataDriven
  *   Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven
- XML 構成ファイル WDTFTest .xml を使用する2つのユーティリティ DLL。
  *   Utility_DeviceStatusCheck_DataDriven
  *   Utility_EnableDisableDriverVerifier_DataDriven
- XML 構成ファイルは次のとおりです。
      *   WDTFTest .xml

**システムデバイス i/o テスト**
-   バイナリ: Sysfund_Device_IO_DataDriven
-   このテストは、システム上のすべてのデバイスに i/o を送信します

**システム-PNP (無効化および有効化) と IO の前後 (信頼性)**
-   バイナリ: Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven
-   [ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/b2849bf1-3478-4fd7-a577-31001084e908)

**システム-PNP デバイステスト (信頼性)**
-   バイナリ: Sysfund_PNP_RemoveAndRestartDevice_DataDriven
-   [ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/ead2222e-4485-4bfc-84cd-43ac0d2e8181)

**システム-(信頼性) 中に IO を使用して再起動する**
-   バイナリ: Sysfund_RebootRestart_With_IO_During_DataDriven
-   [ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/6d6ed5ec-1765-4569-a7ac-20ed7869d89a)

**システム-IO の前後 (信頼性 SysFund)** 
-   バイナリ: Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven
-   [ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/16ac817e-b042-4679-8027-c6c44d1ce29f)

**デバイスの状態の確認**
-   バイナリ: Utility_DeviceStatusCheck_DataDriven
-   このユーティリティ DLL は、ターゲットデバイスの問題コードが 0 (正常に動作している) であることを確認します。  通常は、SysFund テストを実行してターゲットデバイスが正常に動作していることを確認する前に使用されます。

**ドライバーの検証ツールを有効または無効にする**
-   バイナリ: Utility_EnableDisableDriverVerifier_DataDriven
-   このユーティリティは、ターゲットデバイスに関連付けられているドライバーのドライバー検証を有効または無効にします。

**データドリブンテスト構成ファイル**
-   ファイル: WDTFTest .xml
-   このファイルには、データドリブン SysFund テストと関連付けられたユーティリティのすべての構成情報が含まれています。

## <a name="configure-the-tests"></a>テストを構成する

データドリブンテスト構成ファイル (WDTFTest .xml) には、テストおよびユーティリティに渡されるパラメーターを定義するいくつかの要素が含まれています。  すべてのデータドリブンテストおよびユーティリティは、同じ構成ファイル (WDTFTest .xml) を共有します。  既定では、構成ファイルによって、テストとユーティリティがシステム上のすべてのデバイスを対象として構成されますが、これはテストパスの要件に合わせて簡単にカスタマイズできます。

次に示すように、構成ファイルをカスタマイズして、テストやユーティリティがシステム上のすべてのデバイスを対象にし、1つのデバイスまたはドライバーからすべてのデバイスとドライバーを対象とするように設定することができます。

テストとユーティリティは、必要な要素のみを使用し、他のすべての要素は無視します。
### <a name="wdtftestxml-parameter-descriptions-and-use"></a>WDTFTest .xml パラメーターの説明と使用
#### <a name="configuring-the-sdel-query"></a>SDEL クエリの構成
[Sdel 言語](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)は、テストとユーティリティの対象となるデバイスを返すクエリを作成するために使用されます。 ステートメントとステートメントを使用して、次の SDEL 関連のパラメーターを組み合わせて、完全なクエリを作成します。

**Sdel**: 値*isdevice*は、システム上のデバイスの完全なセットを指定します。  通常、特定のドライバーまたはデバイスのみをテストする場合を除き、このパラメーターは編集されません。  次の SDEL 関連のパラメーターでは、テストから除外するドライバーまたはデバイスを指定することによって、このスーパーセットからデバイスのサブセットを作成します。そのため、このパラメーターは変更せずに残すことができます。
```
    <Parameter Name="SDEL">IsDevice</Parameter>
```

**SdelExcludeVMDevnode**: VM 操作にとって重要なデバイスノードは除外され、無効にすることはできません。  このパラメーターは、システムが仮想マシンでない場合には影響を与えないため、変更されないままにしておく必要があります。
```
    <Parameter Name="SdelExcludeVMDevnode">(DisplayName!='Microsoft Hyper-V Virtual Machine Bus')</Parameter>
```

**Sdelexcludedrivers**: sdel を使用してドライバーやデバイスを除外する場合に推奨される場所です。  たとえば、既知のバグがあるドライバーを除外したり、テストの範囲を絞り込んだりすることができます。  既定の ```(DriverBinaryNames!='')``` を使用して実行すると、システム上のすべてのデバイスのすべてのドライバーが対象となります (前述の "Microsoft Hyper-V 仮想マシンバス" デバイスノードを除く)。
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

#### <a name="general-test-configuration-parameters"></a>一般的なテスト構成パラメーター
**Testcycles**: テストを実行するイテレーションの数を指定します。
```
    <Parameter Name="TestCycles">1</Parameter>
```

**IOPeriod**I/o を実行する時間 (分) を指定します。
```
    <Parameter Name="IOPeriod">1</Parameter>
```

**ResumeDelay**: スリープ状態から再開した後に i/o を送信するまでの待機時間を秒数で指定します。
```
    <Parameter Name="ResumeDelay">10</Parameter>
```

**Wpa2PskAesSsid**: テスト WiFi アクセスポイントの名前を指定します。
```
    <Parameter Name="Wpa2PskAesSsid">WiFiRouterName</Parameter>
```

**Wpa2PskPassword**: テスト WiFi アクセスポイントのパスワードを指定します。
```
    <Parameter Name="Wpa2PskPassword">WiFiRouterPassword</Parameter>
```

#### <a name="parameters-that-apply-to-utility_enabledisabledriververifier_datadrivendll-only"></a>```utility_enabledisabledriververifier_datadriven.dll``` にのみ適用されるパラメーター:

**DriverVerifierLevel**: "0x209BB" の既定値は、[ドライバー検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)機能の "標準フラグ" に相当します。
```
    <Parameter Name="DriverVerifierLevel">0x209BB</Parameter>
```

**Addonly**: 結果の sdel クエリの結果が、ドライバーの検証ツールにドライバーを追加する必要があることを指定します。  これは、ドライバーの検証ツールが既にドライバーのセットで有効になっている場合に、置き換えるのではなく、追加する必要がある場合に便利です。
```
    <Parameter Name="AddOnly">false</Parameter>
```

**NoReboot**: ドライバーの検証機能の設定を有効にするために、コンピューターを自動的に再起動しないように指定します。  *NoReboot*パラメーターが true に設定されている場合、拡張されたドライバーの検証ツールの設定は、マシンが手動で再起動されるまで有効になりません。
```
    <Parameter Name="NoReboot">false</Parameter>
```

### <a name="enable-driver-verifier"></a>ドライバーの検証ツールを有効にする
ドライバーの検証を有効にするには、次のコマンドを実行します。
```
    te.exe utility_enabledisabledriververifier_datadriven.dll /name:Utility_DriverVerifier#0::EnableDriverVerifier /rebootstatefile=state.xml 
```
場合によっては、コンピューターが再起動しないことがあります。  これは、テストフレームワークの既知の技術的な制限です。  このユーティリティを使用してドライバーの検証の設定を変更した後、30秒以内にコンピューターの再起動が開始されない場合は、更新されたドライバーの検証ツールの設定を有効にするために、コンピューターを手動で再起動する必要があります。

再起動後に、コマンドプロンプトを開き、 **verifier/querysettings**を実行してドライバーの検証機能が有効になっていることを確認します。

### <a name="verify-devices-are-working"></a>デバイスが動作していることを確認する
データドリブン SysFund テストでは、テストの対象となるすべてのデバイスに問題コード 0 (正常に動作) があることが想定されています。  対象となるすべてのデバイスが正常に動作していることを確認するには、DeviceStatusCheck ユーティリティを使用します。
```
    te.exe Utility_DeviceStatusCheck_DataDriven.dll
```
このユーティリティでは、WDTFTest .xml に定義されている SDEL クエリを使用して、テスト対象のデバイスのセットを検索し、それらのすべてに**問題コード 0**があることを確認します。  "成功" の結果とは、照会されたデバイスのセットがすべて正常に機能していることを意味します。 **Testtextlog .log**を確認して、エラーを調査します。  デバイスマネージャー問題コードの説明については、「[デバイスマネージャーのエラーメッセージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)」を参照してください。

### <a name="launch-a-test"></a>テストの開始
データドリブン SysFund テストを開始するには、次のコマンドを使用します。
```
    te.exe Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
```
```
    te.exe Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
```
### <a name="refine-the-configuration-file"></a>構成ファイルを調整する
変更を行う前に、WDTFTest .xml の元のコピーをバックアップする必要があります。

テスト構成ファイル (WDTFTest .xml) は、データドリブン SysFund テストの結果に基づいて絞り込むことができます。  たとえば、データドリブン SysFund テストが最初にシステム上のすべてのデバイスを対象として実行され、1つの特定のデバイスまたはドライバーがテストに失敗した場合、テスト構成ファイルを更新して、バグの調査中にそのデバイスのテストをフィルターで除外できます。  これにより、バグの調査中にテストを並列で続行できます。

特定のデバイスをフィルターで除外するには、WDTFTest .xml の**Sdelexcludedrivers**要素を編集します。  次のコードは、 *mydriver*をフィルターで除外します。次に例を示します。 
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver.sys’)</Parameter>
```

同様に、次のコードはデバイスのインスタンスパスに基づいてデバイスを除外します。
```
<Parameter Name="SdelExcludeDrivers">(DeviceId!=’my\device\id’)</Parameter>
```
複雑な SDEL クエリを作成して、複数のデバイスを除外することができます。
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver1.sys’ AND DriverBinaryNames!=’mydriver2.sys’)</Parameter>
```

Mydriver1 と mydriver2 でバグを修正した後、WDTFTest .xml の**Sdelexcludedrivers**要素を既定値にリセットして、これらのドライバーと関連付けられているデバイスをターゲットとして含めることができます。
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

## <a name="troubleshooting-problems"></a>問題のトラブルシューティング
### <a name="malformed-sdel-query-in-the-configuration-file"></a>構成ファイルの無効な形式の SDEL クエリ
次のエラーメッセージは、WDTFTest .xml 構成ファイルに含まれている不適切な形式の SDEL クエリを示しています。
```
    Error: Verify: SUCCEEDED(m_pDeviceDepot->Query(CComBSTR(DQ), &m_pTestTargets)) - Value (0x80070057) [File: onecore\base\tools\wdtf\tests\devfund\datadriven\sysfund_pnp_disableenable_with_io_beforeandafter_datadriven\test.cpp, Function: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test, Line: 231]
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#0 [Failed]
```
HRESULT ' 0x80070057 ' は、"E_INVALIDARG: 1 つ以上の引数が無効です" を意味します。 [Sdel ドキュメント](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に対して WDTFTest .xml 構成ファイルを慎重に確認し、このエラーの原因と考えられる間違った形式のクエリを探してください。

### <a name="test-is-blocked-because-it-might-reboot-the-machine"></a>コンピューターを再起動する可能性があるため、テストはブロックされています
特定の SysFund テストでは、テスト中にコンピューターを再起動できます。 コンピューターを再起動できるテストを実行するには、"/rebootstatefile" パラメーターを使用する必要があります。
```
    te.exe <testname> /rebootstatefile=state.xml
```
/Rebootstatefile パラメーターがテストに渡されない場合、次のメッセージが表示され、テストはブロックされます。
```
    TestBlocked: TAEF: This test cannot be run as it might reboot the machine.
    EndGroup: Sysfund_RebootRestart_With_IO_During::Sysfund_RebootRestart_With_IO_During_DataDriven_Test#0 [Blocked]
```

### <a name="test-is-blocked-because-the-sdel-query-contains--characters"></a>SDEL クエリに ' & ' 文字が含まれているため、テストがブロックされています
デバイスインスタンスのパス値に基づいてデバイスを対象とする SDEL クエリを指定するときは、パスの ' & ' 文字を "& amp\;" に置き換える必要があります。 次のメッセージは、デバイスインスタンスパスに ' & ' 文字を含む WDTFTest .xml 構成ファイルを示しています。
```
    TestBlocked: TAEF: [HRESULT: 0xC00CEE22] Error while getting value for 'SDEL' in table 'DataDrivenSysfundTable' in DataSource 'WDTFTest.xml' on line 24.
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#error [Blocked]
```
これは、上記のエラーメッセージを生成する WDTFTest .xml 構成ファイルの XML です。
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```
これは、エラーを修正する deviceid の適切な形式の値です。
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```

### <a name="other-issues"></a>その他の問題
ここに記載されていないその他の問題のトラブルシューティングについては、 [Device. DevFund の追加ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-additional-documentation)を参照してください。

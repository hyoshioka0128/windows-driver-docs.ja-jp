---
title: テストを実行する
description: Windows ドライバーのテストをデータに基づく SysFund のテストと構成ファイルの説明
keywords:
- Sysfund テスト
- データ ドリブン テスト
- SDEL クエリ
ms.date: 11/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf982a69e7e22088bb09eb8380ad5720c1800daf
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161546"
---
# <a name="run-the-tests"></a>テストを実行する
## <a name="description-of-the-tests-and-configuration-file"></a>テストと構成ファイルの説明
データ ドリブン SysFund テストを検索する\<解凍 EWDK ルート > \Program Files\Windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund\DataDriven します。  データ ドリブン テスト スイートは、次のファイルで構成されます。

- 5 つは、WDTFTest.xml XML 構成ファイルを使用する DLL をテストします。

  *   Sysfund_Device_IO_DataDriven.dll
  *   Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
  *   Sysfund_PNP_RemoveAndRestartDevice_DataDriven.dll
  *   Sysfund_RebootRestart_With_IO_During_DataDriven.dll
  *   Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
- 2 つのユーティリティ DLL の WDTFTest.xml XML 構成ファイルを使用します。
  *   Utility_DeviceStatusCheck_DataDriven.dll
  *   Utility_EnableDisableDriverVerifier_DataDriven.dll
- XML 構成ファイル:
      *   WDTFTest.xml

**システム - デバイスの I/O のテスト**
-   バイナリ。Sysfund_Device_IO_DataDriven.dll
-   このテストは、システム上のすべてのデバイスに I/O を送信します。

**システム - PNP (無効および有効にする) と IO (信頼性) の前後**
-   バイナリ。Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
-   [ドキュメント](https://msdn.microsoft.com/de-de/library/windows/hardware/dn941373(v=vs.85).aspx)

**システム - PNP デバイスのテスト (信頼性) の削除します。**
-   バイナリ。Sysfund_PNP_RemoveAndRestartDevice_DataDriven.dll
-   [ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/ead2222e-4485-4bfc-84cd-43ac0d2e8181)

**システム - 途中の IO を伴う再起動 (信頼性)**
-   バイナリ。Sysfund_RebootRestart_With_IO_During_DataDriven.dll
-   [ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/6d6ed5ec-1765-4569-a7ac-20ed7869d89a)

**システムのスリープ (信頼性 SysFund) の前後に IO を** 
-   バイナリ。Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
-   [ドキュメント](https://msdn.microsoft.com/library/windows/hardware/dn940448(v=vs.85).aspx)

**デバイスの状態の確認**
-   バイナリ。Utility_DeviceStatusCheck_DataDriven.dll
-   このユーティリティの DLL は、ターゲット デバイスの問題のコードが 0 (正常に動作) を確認します。  ターゲット デバイスが正常に動作を確認する SysFund テストを実行する前に一般的に使用されます。

**Driver Verifier の有効化/無効化**
-   バイナリ。Utility_EnableDisableDriverVerifier_DataDriven.dll
-   このユーティリティを有効または Driver Verifier をターゲット デバイスに関連付けられているドライバーを無効にします。

**データ ドリブン テストの構成ファイル**
-   ファイル:WDTFTest.xml
-   このファイルには、すべてのデータ ドリブン SysFund テストと関連付けられているユーティリティ構成情報が含まれています。

## <a name="configure-the-tests"></a>テストを構成します。

データ ドリブン テストの構成ファイル (WDTFTest.xml) には、テストとユーティリティに渡されるパラメーターを定義するいくつかの要素が含まれています。  ユーティリティ、データ ドリブン テストのすべては、同じ構成ファイル (WDTFTest.xml) を共有します。  既定では、構成ファイルを構成、テストと、システム上のすべてのデバイスを対象にユーティリティが、これは、テスト パスの要件に合わせて簡単にカスタマイズできます。

以下に示すため、テストとユーティリティに 1 つのデバイスまたはすべてのデバイスとドライバーをドライバーから、システム上のデバイスのセットを対象に、構成ファイルをカスタマイズできます。

テストとユーティリティは、必要な要素のみを使用し、他のすべての要素は無視されます。
### <a name="wdtftestxml-parameter-descriptions-and-use"></a>WDTFTest.xml パラメーターの説明と使用
#### <a name="configuring-the-sdel-query"></a>SDEL クエリを構成します。
[SDEL 言語](https://msdn.microsoft.com/library/windows/hardware/ff538361%28v=vs.85%29.aspx)をテストおよびユーティリティの対象となるデバイスを返すクエリを作成するために使用します。 完全なクエリを作成してステートメントを使用して次の SDEL 関連パラメーターを表示するには。

**SDEL**:値*IsDevice*システム上のデバイスの完全なセットを指定します。  通常、特定のドライバーまたはデバイスをテストする場合を除き、このパラメーターは編集できません。  SDEL 関連の次のパラメーターはドライバーを指定することによってこのスーパー セットからデバイスのサブセットを作成する、またはこのパラメーターは省略可能であるため、テストから除外する対象のデバイスが変更されません。
```
    <Parameter Name="SDEL">IsDevice</Parameter>
```

**SdelExcludeVMDevnode**:VM の操作に不可欠な無効にすることはできませんをデバイス ノードを除外します。  このパラメーターを残しておく必要がある影響を与えませんシステムが仮想マシンではない場合、変更されません。
```
    <Parameter Name="SdelExcludeVMDevnode">(DisplayName!='Microsoft Hyper-V Virtual Machine Bus')</Parameter>
```

**SdelExcludeDrivers**: これは、ドライバーやデバイスを除外する SDEL を使用するをお勧めします。  たとえば、既知のバグがあるドライバーを除外するか、テストの範囲を絞り込むにこれを使用する可能性があります。  既定値は実行されている```(DriverBinaryNames!='')```(「Microsoft HYPER-V 仮想マシン バス」デバイス ノード上に示した) を除く、システム上のすべてのデバイスのすべてのドライバーを対象とします。
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

#### <a name="general-test-configuration-parameters"></a>一般的なテスト構成パラメーター
**TestCycles**:テストを実行する必要があります反復回数を指定します。
```
    <Parameter Name="TestCycles">1</Parameter>
```

**IOPeriod**分 I/O を実行する必要がありますを指定します。
```
    <Parameter Name="IOPeriod">1</Parameter>
```

**ResumeDelay**:復帰後の I/O を送信する前に待機する秒数がスリープ状態を指定します。
```
    <Parameter Name="ResumeDelay">10</Parameter>
```

**Wpa2PskAesSsid**:テストの WiFi アクセス ポイントの名前を指定します。
```
    <Parameter Name="Wpa2PskAesSsid">WiFiRouterName</Parameter>
```

**Wpa2PskPassword**:テストの WiFi アクセス ポイントのパスワードを指定します。
```
    <Parameter Name="Wpa2PskPassword">WiFiRouterPassword</Parameter>
```

#### <a name="parameters-that-apply-to-utilityenabledisabledriververifierdatadrivendll-only"></a>パラメーターに適用される```utility_enabledisabledriververifier_datadriven.dll```のみ。

**DriverVerifierLevel**:0x209BB の既定値はの「標準フラグ」と等しい[Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)します。
```
    <Parameter Name="DriverVerifierLevel">0x209BB</Parameter>
```

**AddOnly**:結果として得られる SDEL クエリの結果が削除することがなく、Driver Verifier にドライバーを追加する必要があることを指定します。  これは、Driver Verifier は、一連のドライバーをなくするように追加交換で既に有効な場合に便利です。
```
    <Parameter Name="AddOnly">false</Parameter>
```

**NoReboot**:マシンは、Driver Verifier の設定を有効に自動的に再起動しない必要がありますを指定します。  場合、 *NoReboot*パラメーターが設定されている拡張の Driver Verifier を true に設定が有効になりません、マシンを手動で再起動するまでです。
```
    <Parameter Name="NoReboot">false</Parameter>
```

### <a name="enable-driver-verifier"></a>ドライバーの検証を有効にします。
ドライバーの検証を有効にするには、次のコマンドを実行します。
```
    te.exe utility_enabledisabledriververifier_datadriven.dll /name:Utility_DriverVerifier#0::EnableDriverVerifier /rebootstatefile=state.xml 
```
特定のインスタンスでは、コンピューターが再起動されません。  これは、テスト フレームワークの既知の技術的な制限です。  マシンがこのユーティリティを使用したドライバーの検証設定を変更した後、30 秒以内に再起動を開始していない場合は、更新されたドライバーの検証設定を有効にするためにコンピューターを手動で再起動する必要があります。

再起動後、コマンド プロンプトを開き、実行**verifier/querysettings** Driver Verifier を有効になっていることを確認します。

### <a name="verify-devices-are-working"></a>デバイスが正常に機能を確認します。
SysFund のデータ ドリブン テストには、0 (正常に動作) の問題のコードにテストの対象となるすべてのデバイスが期待しています。  正常に動作している対象となるすべてのデバイスを確認するには、DeviceStatusCheck ユーティリティを使用します。
```
    te.exe Utility_DeviceStatusCheck_DataDriven.dll
```
このユーティリティでは、WDTFTest.xml で定義されている SDEL クエリを使用して、一連のテスト対象のデバイスを検索し、すべてがあることを確認**問題コード 0**します。  「成功」の結果は、一連のクエリを実行するデバイスは、すべての操作が正しくを意味します。 レビュー **TestTextLog.log**エラーを調査します。  デバイス マネージャーの問題のコードの詳細については、次を参照してください。[デバイス マネージャーのエラー メッセージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)します。

### <a name="launch-a-test"></a>テストを起動します。
SysFund のデータ ドリブン テストのいずれかを起動するには、次のコマンドを使用します。
```
    te.exe Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
```
```
    te.exe Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
```
### <a name="refine-the-configuration-file"></a>構成ファイルを絞り込む
変更を加える前に、WDTFTest.xml の元のコピーをバックアップする必要があります。

テスト構成ファイル (WDTFTest.xml) は、SysFund のデータ ドリブン テストの結果に基づいて、洗練されたであることができます。  など、システム上のすべてのデバイスを対象とするデータ ドリブンの SysFund テストが最初に実行、1 つの特定のデバイスまたはドライバーには、テストが失敗した場合は、テストの構成ファイルは、バグの調査中にそのデバイスのテストをフィルターで除外を更新できます。  これにより、バグ、調査中に、並列で引き続きテストできます。

特定のデバイスをフィルターで除外、編集、 **SdelExcludeDrivers** WDTFTest.xml 内の要素。  次のコードでフィルター アウト*mydriver.sys*など。 
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver.sys’)</Parameter>
```

同様に、次のコード フィルター アウト デバイス インスタンスのパスに基づくデバイス。
```
<Parameter Name="SdelExcludeDrivers">(DeviceId!=’my\device\id’)</Parameter>
```
複数のデバイスのフィルターで除外する複雑な SDEL クエリを作成できます。
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver1.sys’ AND DriverBinaryNames!=’mydriver2.sys’)</Parameter>
```

Mydriver1.sys と mydriver2.sys でバグを修正した後にリセットできます、 **SdelExcludeDrivers**にこれらのドライバーと関連付けられているデバイスのターゲットとして含める既定値に WDTFTest.xml 内の要素。
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

## <a name="troubleshooting-problems"></a>問題のトラブルシューティング
### <a name="malformed-sdel-query-in-the-configuration-file"></a>構成ファイルの形式が正しくない SDEL クエリ
次のエラー メッセージは不適切に作成された SDEL クエリ WDTFTest.xml の構成ファイルに含まれるを示しています。
```
    Error: Verify: SUCCEEDED(m_pDeviceDepot->Query(CComBSTR(DQ), &m_pTestTargets)) - Value (0x80070057) [File: onecore\base\tools\wdtf\tests\devfund\datadriven\sysfund_pnp_disableenable_with_io_beforeandafter_datadriven\test.cpp, Function: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test, Line: 231]
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#0 [Failed]
```
HRESULT '0x80070057' 意味"E_INVALIDARG:1 つまたは複数の引数が無効です"。 に対して WDTFTest.xml 構成ファイルを慎重に確認、 [SDEL ドキュメント](https://msdn.microsoft.com/library/windows/hardware/ff538361%28v=vs.85%29.aspx)しこのエラーの原因となる形式が正しくないクエリを探します。

### <a name="test-is-blocked-because-it-might-reboot-the-machine"></a>テストがブロックされているため、マシンを再起動する可能性があります。
特定 SysFund のテストは、テスト中に、コンピューターを再起動することができます。 コンピューターを再起動することができるテストを実行するには、"/rebootstatefile"パラメーターを使用する必要があります。
```
    te.exe <testname> /rebootstatefile=state.xml
```
/Rebootstatefile パラメーターがテストに渡されないと、次のメッセージが表示され、テストはブロックされます。
```
    TestBlocked: TAEF: This test cannot be run as it might reboot the machine.
    EndGroup: Sysfund_RebootRestart_With_IO_During::Sysfund_RebootRestart_With_IO_During_DataDriven_Test#0 [Blocked]
```

### <a name="test-is-blocked-because-the-sdel-query-contains--characters"></a>テストがブロックされているため、SDEL クエリを含む ' &' の文字
ときにかどうか、そのデバイス インスタンスのパス値に基づいて、デバイスをターゲットと SDEL クエリ '&'、パス内の文字に置き換える必要があります"(& a) amp\;"。 次のメッセージは格納 ' &' のデバイスのインスタンスのパス内の文字 WDTFTest.xml 構成ファイルを示しています。
```
    TestBlocked: TAEF: [HRESULT: 0xC00CEE22] Error while getting value for 'SDEL' in table 'DataDrivenSysfundTable' in DataSource 'WDTFTest.xml' on line 24.
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#error [Blocked]
```
これは、上記のエラー メッセージを生成した WDTFTest.xml 構成ファイルから XML です。
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```
これは、エラーを修正する deviceid の整形式の値です。
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```

### <a name="other-issues"></a>その他の問題
この一覧にないその他の問題のトラブルシューティングについては、次を参照してください。 [Device.DevFund その他のドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-additional-documentation)します。

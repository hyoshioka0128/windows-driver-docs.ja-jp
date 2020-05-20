---
ms.assetid: D4B7FC2A-259F-4B72-A52B-03CBF712D5C5
title: ユニバーサル Windows ドライバーの検証
description: ApiValidator.exe ツールを使うと、ドライバーから呼び出される API が、ユニバーサル Windows ドライバーにとって有効であるかどうかを確認できます。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5884d843d5f1ca25440ace35982f9051ac902774
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270453"
---
# <a name="validating-windows-drivers"></a>Windows ドライバーの検証

InfVerif および ApiValidator ツールを使用して、「[Windows ドライバーの概要](getting-started-with-windows-drivers.md)」で説明されている要件に従って Windows ドライバーをテストします。

## <a name="infverif"></a>InfVerif

[InfVerif](../devtest/infverif.md) は、INF 構文を検証し、INF が要件と制限に準拠していることを確認するツールです。

`/w` および `/v` と共に InfVerif を使用して、Windows ドライバーについて以下の点を確認します。

* **DCH 設計原則**の[宣言型 (D)](dch-principles-best-practices.md) 原則を満たしているか
* 「[Windows ドライバーの概要](getting-started-with-windows-drivers.md)」の[ドライバー パッケージの分離](driver-isolation.md)要件に準拠しているか

詳細については、「[コマンドラインからの InfVerif の実行](../devtest/running-infverif-from-the-command-line.md)」を参照してください。 

## <a name="apivalidator"></a>ApiValidator

ApiValidator ツールを使うと、バイナリから呼び出される API が、Windows ドライバーにとって有効であるかどうかを確認できます。 Windows ドライバーにとって有効な API セットの外部にある API をバイナリが呼び出すと、エラーが返されます。 このツールは、WDK for Windows 10 の一部です。

ApiValidator では、[API レイヤー化](api-layering.md) (Windows ドライバーの要件の 1 つ) がドライバーでサポートされているかを検証します。 要件の完全な一覧については、「[Windows ドライバーの概要](getting-started-with-windows-drivers.md)」を参照してください。

### <a name="running-apivalidator-in-visual-studio"></a>Visual Studio での ApiValidator の実行

ドライバー プロジェクトの **[ターゲット プラットフォーム]** プロパティが **[Windows ドライバー]** に設定されていれば、Visual Studio はビルド後の手順として自動的に ApiValidator を実行します。

ApiValidator で表示されたメッセージをすべて確認するには、 **[ツール]、[オプション]、[プロジェクトおよびソリューション]、[ビルド/実行]** の順に移動して、 **[MSBuild プロジェクト ビルドの出力の詳細]** を **[詳細]** に設定します。 コマンド ラインからビルドする場合は、ビルド コマンドに **/v:detailed** スイッチまたは **/v:diag** スイッチを追加すると、詳しい出力を得ることができます。

umdf2_fx2 ドライバー サンプルに対して API の検証を実行すると、次のようなエラーが表示されます。

```cpp
Warning  1   warning : API DecodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 2   warning : API DisableThreadLibraryCalls in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 3   warning : API EncodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 4   warning : API GetCurrentProcessId in kernel32.dll is not supported. osrusbfx2um.dll calls this API. C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 5   warning : API GetCurrentThreadId in kernel32.dll is not supported. osrusbfx2um.dll calls this API.  C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 6   warning : API GetSystemTimeAsFileTime in kernel32.dll is not supported. osrusbfx2um.dll calls this API. C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 7   warning : API IsDebuggerPresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 8   warning : API IsProcessorFeaturePresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.   C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Warning 9   warning : API QueryPerformanceCounter in kernel32.dll is not supported. osrusbfx2um.dll calls this API. C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe    osrusbfx2um
Error   10  error MSB3721: The command ""C:\Program Files (x86)\Windows Kits\10\bin\x64\ApiValidator.exe" -DriverPackagePath:"C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\Debug\\" -SupportedApiXmlFiles:"C:\Program Files (x86)\Windows Kits\10\build\universalDDIs\x86\UniversalDDIs.xml" -ApiExtractorExePath:"C:\Program Files (x86)\Windows Kits\10\bin\x64"" exited with code -1.    C:\Program Files (x86)\Windows Kits\10\build\WindowsDriver.common.targets   1531    5   osrusbfx2um
```

### <a name="fixing-validation-errors"></a>検証エラーの修正

1.  レガシ デスクトップ UMDF ドライバー プロジェクトを　Windows ドライバーに切り替えた場合は、バイナリをビルドするときに、適切なライブラリが含まれていることを確認します。 プロジェクトを右クリックし、プロパティを選択します。 **[リンカー]、[入力]** の順に移動します。 **[追加の依存ファイル]** に次のものが含まれている必要があります。

    ```cpp
    %AdditionalDependencies);$(SDK_LIB_PATH)\OneCoreUAP.lib
    ```

    OneCore SKU をターゲットとするためのリンカー オプションを確認するには、「[OneCore をターゲットとしたビルド](building-for-onecore.md)」をご覧ください。

2.  許可されない API の呼び出しを一度に 1 つずつ削除または置換し、エラーがなくなるまでツールを再実行します。

3.  このような呼び出しは、デスクトップ専用 DDI のリファレンス ページに記載されている代替 DDI への置き換えが可能な場合があります。 適切な代替インターフェイスが見つからない場合は、[フィードバックを送信](https://go.microsoft.com/fwlink/p/?linkid=529549)してお知らせください。  適切な代替インターフェイスが存在しない場合は、回避策のコーディングが必要になることがあります。  必要に応じて、WDK のドライバー テンプレートから新しい Windows ドライバーを作成してください。

次のようなエラーが発生する場合は、「[OneCore をターゲットとしたビルド](building-for-onecore.md)」のガイダンスを参照してください。

```cpp
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSEnumerateSessionsW' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSFreeMemory' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: NOT all binaries are Universal
```

### <a name="running-apivalidator-from-the-command-prompt"></a>コマンド プロンプトからの ApiValidator の実行

Apivalidator.exe をコマンド プロンプトで実行することもできます。 WDK インストールで、**C:\Program Files (x86)\Windows Kits\10\bin\<arch>** と **C:\Program Files (x86)\Windows Kits\10\build\universalDDIs\<arch>** に移動します。 

**重要な注意:**
* ApiValidator には次のファイルが必要です。ApiValidator.exe、Aitstatic.exe、Microsoft.Kits.Drivers.ApiValidator.dll、および UniversalDDIs.xml。 
* UniversalDDIs.xml は、検証されるバイナリ アーキテクチャと一致する必要があります。たとえば、x64 ドライバーの場合は x64 UniversalDDI.xml を使用します。
* ApiValidator でテストされるのは、一度に 1 つのアーキテクチャのみになります。
* その他の情報については、以下の ApiValidator に関する既知の問題を参照してください。

使用する構文は以下のとおりです。

`Apivalidator.exe -DriverPackagePath: <driver folder path> -SupportedApiXmlFiles: (path to XML files containing supported APIs for Windows drivers)`

たとえば、WDK のアクティビティ サンプルから呼び出される API を検証するには、まず Visual Studio でサンプルをビルドします。 次に、コマンド プロンプトを開き、ツールが存在するディレクトリ (例: `C:\Program Files (x86\Windows Kits\10\bin\x64`) に移動します。 次のコマンドを入力します。

`apivalidator.exe -DriverPackagePath:"C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2\_fx2\Debug" -SupportedApiXmlFiles:"c:\Program Files (x86)\Windows Kits\10\build\universalDDIs\x64\UniversalDDIs.xml"`

このコマンドを実行すると、次の出力が生成されます。

```cpp
ApiValidator.exe: Warning: API DecodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API DisableThreadLibraryCalls in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API EncodePointer in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API GetCurrentProcessId in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API GetCurrentThreadId in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API GetSystemTimeAsFileTime in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API IsDebuggerPresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API IsProcessorFeaturePresent in kernel32.dll is not supported. osrusbfx2um.dll calls this API.
ApiValidator.exe: Warning: API QueryPerformanceCounter in kernel32.dll is not supported. osrusbfx2um.dll calls this API.

ApiValidator.exe Driver located at C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\Debug is NOT a Universal Driver
```

### <a name="troubleshooting-apivalidator"></a>ApiValidator のトラブルシューティング


ApiValidator.exe で、形式が正しくないことを示す次のようなエラーが出力された場合:

```cpp
Error      1              error : AitStatic output file has incorrect format or analysis run on incorrect file types.     C:\Program Files (x86)\Windows Kits\10\src\usb\umdf2_fx2\driver\ApiValidator.exe            osrusbfx2um
```

次の回避策を実行します。

1.  プロジェクトのプロパティを開き、 **[全般]** に移動して、 **[出力ディレクトリ]** の名前を次のように変更します。

    ```cpp
    $(SolutionDir)$(Platform)\$(ConfigurationName)\
    ```

2.  ソリューションをリビルドします。

### <a name="known-apivalidator-issues"></a>ApiValidator に関する既知の問題

* ARM64 では AitStatic が動作しないため、ApiValidator は ARM64 では実行されません。
* ARM64 のバイナリは x64 コンピューターではテストできますが、x86 コンピューターではできません。
* ApiValidator を x86 上で実行して、x86 のバイナリと ARM のバイナリをテストできます。
* ApiValidator を x64 上で実行して、x86、x64、ARM、ARM64 のバイナリをテストできます。




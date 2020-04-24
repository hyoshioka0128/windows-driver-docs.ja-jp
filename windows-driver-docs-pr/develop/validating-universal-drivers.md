---
ms.assetid: D4B7FC2A-259F-4B72-A52B-03CBF712D5C5
title: ユニバーサル Windows ドライバーの検証
description: ApiValidator.exe ツールを使うと、ドライバーから呼び出される API が、ユニバーサル Windows ドライバーにとって有効であるかどうかを確認できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78b5827d01525464f5660e863bf48c7a3e66ae21
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63344036"
---
# <a name="validating-universal-windows-drivers"></a>ユニバーサル Windows ドライバーの検証

ApiValidator.exe ツールを使うと、バイナリから呼び出される API が、ユニバーサル Windows ドライバーにとって有効であるかどうかを確認できます。 ユニバーサル Windows ドライバーにとって有効な API セットの外部にある API をバイナリが呼び出すと、エラーが返されます。 このツールは、Windows Driver Kit (WDK) for Windows 10 の一部です。

## <a name="span-idrunning_apivalidator_in_visual_studiospanspan-idrunning_apivalidator_in_visual_studiospanspan-idrunning_apivalidator_in_visual_studiospanrunning-apivalidator-in-visual-studio"></a><span id="Running_ApiValidator_in_Visual_Studio"></span><span id="running_apivalidator_in_visual_studio"></span><span id="RUNNING_APIVALIDATOR_IN_VISUAL_STUDIO"></span>Visual Studio での ApiValidator の実行


ドライバー プロジェクトの **[ターゲット プラットフォーム]** プロパティが **[ユニバーサル]** に設定されていれば、Visual Studio はビルド後の手順として自動的に ApiValidator を実行します。

ApiValidator で表示されたメッセージをすべて確認するには、 **[ツール] &gt; [オプション] &gt; [プロジェクトおよびソリューション] &gt; [ビルド/実行]** の順に移動して、 **[MSBuild プロジェクト ビルドの出力の詳細]** を **[詳細]** に設定します。 コマンド ラインからビルドする場合は、ビルド コマンドに **/v:detailed** スイッチまたは **/v:diag** スイッチを追加すると、詳しい出力を得ることができます。

umdf2\_fx2 ドライバー サンプルに対して API の検証を実行すると、次のようなエラーが表示されます。

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

## <a name="fixing-validation-errors"></a>検証エラーの修正

1.  レガシ デスクトップ UMDF ドライバー プロジェクトをユニバーサルに切り替えた場合は、バイナリをビルドするときに、適切なライブラリが含まれていることを確認します。 プロジェクトを右クリックし、プロパティを選択します。 **[リンカー] &gt; [入力]** の順に移動します。 **[追加の依存ファイル]** に次のものが含まれている必要があります。

    ```cpp
    %AdditionalDependencies);$(SDK_LIB_PATH)\OneCoreUAP.lib
    ```

    OneCore SKU をターゲットとするためのリンカー オプションを確認するには、「[OneCore をターゲットとしたビルド](building-for-onecore.md)」をご覧ください。

2.  非ユニバーサル API の呼び出しを一度に 1 つずつ削除または置換し、エラーがなくなるまでツールを再実行します。

3.  このような呼び出しは、デスクトップ専用 DDI のリファレンス ページに記載されている代替 DDI への置き換えが可能な場合があります。 適切な代替インターフェイスが見つからない場合は、[フィードバックを送信](https://go.microsoft.com/fwlink/p/?linkid=529549)してお知らせください。  適切な代替インターフェイスが存在しない場合は、回避策のコーディングが必要になることがあります。  必要に応じて、WDK のドライバー テンプレートから新しいユニバーサル Windows ドライバーを作成してください。

次のようなエラーが発生する場合は、「[OneCore をターゲットとしたビルド](building-for-onecore.md)」のガイダンスを参照してください。

```cpp
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSEnumerateSessionsW' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: Error: FlexLinkTest.exe has a dependency on 'wtsapi32.dll!WTSFreeMemory' but is missing: IsApiSetImplemented("ext-ms-win-session-wtsapi32-l1-1-0")
ApiValidation: NOT all binaries are Universal
```

## <a name="running-apivalidator-from-the-command-prompt"></a>コマンド プロンプトからの ApiValidator の実行

Apivalidator.exe をコマンド プロンプトで実行することもできます。 WDK のインストールで、C:\\Program Files (x86)\\Windows Kits\\10\\bin\\ *&lt;arch&gt;* に移動します。

使用する構文は以下のとおりです。

**Apivalidator.exe** **-DriverPackagePath:** _&lt;ドライバー フォルダーのバス&gt;_  
 **-SupportedApiXmlFiles:** _&lt;サポートされるユニバーサル ドライバー用の API を含む XML ファイルのパス&gt;_

たとえば、WDK のアクティビティ サンプルから呼び出される API を検証するには、まず Visual Studio でサンプルをビルドします。 次に、コマンド プロンプトを開き、ツールが存在するディレクトリ (例: C:\\Program Files (x86)\\Windows Kits\\10\\bin\\x64) に移動します。 次のコマンドを入力します。

**apivalidator.exe -DriverPackagePath:"C:\\Program Files (x86)\\Windows Kits\\10\\src\\usb\\umdf2\_fx2\\Debug\\\\" -SupportedApiXmlFiles:"c:\\Program Files (x86)\\Windows Kits\\10\\build\\universalDDIs\\x64\\UniversalDDIs.xml"**

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

ユニバーサル Windows ドライバーの有効な API を列挙した XML ファイルは、C:\\Program Files (x86)\\Windows Kits\\10\\build\\universalDDIs\\ *&lt;arch&gt;* にあります。

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting"></a><span id="Troubleshooting"></span><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>トラブルシューティング


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

## <a name="known-issues"></a>既知の問題

* ARM64 では AitStatic が動作しないため、ApiValidator は ARM64 では実行されません。
* ARM64 のバイナリは x64 コンピューターではテストできますが、x86 コンピューターではできません。
* ApiValidator を x86 上で実行して、x86 のバイナリと ARM のバイナリをテストできます。
* ApiValidator を x64 上で実行して、x86、x64、ARM、ARM64 のバイナリをテストできます。



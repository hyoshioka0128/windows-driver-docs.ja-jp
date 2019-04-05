---
ms.assetid: 31CE7AE9-6444-4706-9C43-2B35038FA955
title: コマンド プロンプトから実行時にドライバーをテストする方法
description: WDK には、ネットワーク上のテスト コンピューターでドライバーをテストできるように、デバイス テスト コンポーネントが用意されています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f1b2c59d6a9da5abdd8e614650a6234aa03b4a3
ms.sourcegitcommit: 672bf3fd18f6c169b5634476613ce1da9250413b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2019
ms.locfileid: "58898061"
---
# <a name="how-to-test-a-driver-at-runtime-from-a-command-prompt"></a>コマンド プロンプトから実行時にドライバーをテストする方法

WDK には、ネットワーク上のテスト コンピューターでドライバーをテストできるように、デバイス テスト コンポーネントが用意されています。 これらのコンポーネントは、必要なファイルをコピーしてインストールすることで、Visual Studio 以外でも使うことができます。 これらのコンポーネントを使うと、Visual Studio にあるのと同じコレクションのデバイス ドライバー テストを実行して、ドライバーの機能をテストできます。

WDK 8.1 以降、コマンド スクリプトを使って、テスト コンピューターで HCK テスト スイートをコピーおよび実行できるようになりました。 「[WDK 8.1 の HCK テスト スイートを実行する方法](run-the-hck-test-suites-in-the-wdk.md)」をご覧ください。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件

-   Visual Studio と WDK を開発用のコンピューターにインストールします。
-   Visual Studio から、テスト用のコンピューターの構成とプロビジョニングを行うことができます。 テスト コンピューターを構成すると、WDK ドライバー テスト フレームワークは自動的にテスト コンピューターのリモート デバッグを有効にして、必要なテスト バイナリとサポート ファイルを転送します。 まだ準備ができていない場合は、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)」の指示に従ってください。
-   お勧めしませんが、必要なテスト コンポーネントを手動でインストールすることもできます。 指示に従って、[Test Authoring and Execution Framework (TAEF)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439725) と WDTF をテスト コンピューターにインストールします。 「[手動によるテスト コンピューターへの TAEF のインストールとアンインストール](https://msdn.microsoft.com/Library/Windows/Hardware/hh439627#manual_install_taef)」と「[手動によるテスト コンピューターへの WDTF のインストール](https://msdn.microsoft.com/Library/Windows/Hardware/hh831856#manual_install_wdtf)」をご覧ください。

<a name="instructions"></a>手順
------------

### <a name="span-idcopytheteststothetestcomputerspanspan-idcopytheteststothetestcomputerspanspan-idcopytheteststothetestcomputerspanstep-1-copy-the-tests-to-the-test-computer"></a><span id="Copy_the_tests_to_the_test_computer"></span><span id="copy_the_tests_to_the_test_computer"></span><span id="COPY_THE_TESTS_TO_THE_TEST_COMPUTER"></span>ステップ 1:テスト コンピューターにテストをコピーする

-   [Device Fundamental のテスト](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673011)を開発用のコンピューターからコピーします。 フォルダー %ProgramFiles%\\Windows Kits\\8.0\\Testing\\Tests\\Device Fundamentals をテスト コンピューターにコピーします。

### <a name="span-idrunthetestsspanspan-idrunthetestsspanspan-idrunthetestsspanstep-2-run-the-tests"></a><span id="Run_the_tests"></span><span id="run_the_tests"></span><span id="RUN_THE_TESTS"></span>ステップ 2:テストを実行する

テストを実行する TAEF コマンドでは次の構文を使います。

```cpp
Te.exe [/name:<Test Method>] [<Test Name>.dll | <Test Name.wsc> ]  [/rebootStateFile=<file> ] [/enablewttlogging]  [/P:"DQ= <>" ]  
```

<a name="remarks"></a>注釈
-------

テスト バイナリ (.dll) ファイルまたはスクリプト (.wsc) ファイルを指定する必要があります。 テスト メソッド (**/name:**_&lt;テスト メソッド&gt;_) は省略可能です。 テスト名とテスト メソッドについては、「[Device Fundamental のテスト](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673011)」をご覧ください。 テスト パラメーターの指定方法については、「[Device Fundamental テストのパラメーター](how-to-select-and-configure-the-device-fundamental-tests.md)」と「[Te.exe のコマンド オプション](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439743)」をご覧ください。

たとえば、次のように、特定のデバイス ID を持つデバイスで Devfund\_PnPDTest.dll にあるすべての PnP テストを実行します。

```cpp
Te.exe  Devfund_PnPDTest.dll /P:"DQ=DeviceID='USB\ROOT_HUB\4&1CD5D022&0'"
```

たとえば、次のように、特定のデバイス ID を持つデバイスで突然の削除 PnP テストを実行します。

```cpp
Te.exe /name:"*PNPSurpriseRemoveAndRestartDevice" Devfund_PnPDTest.dll /P:"DQ=DeviceID='USB\ROOT_HUB\4&1CD5D022&0'"
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [Device Fundamental のテスト](https://msdn.microsoft.com/Library/Windows/Hardware/JJ673011)
* [Device Fundamental テストのパラメーター](how-to-select-and-configure-the-device-fundamental-tests.md)
* [WDK 8.1 の HCK テスト スイートを実行する方法](run-the-hck-test-suites-in-the-wdk.md)
* [Test Authoring and Execution Framework (TAEF)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439725)
* [Te.exe のコマンド オプション](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439743)
 

 







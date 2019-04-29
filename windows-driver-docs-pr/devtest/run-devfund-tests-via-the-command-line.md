---
title: コマンド ラインから DevFund テストを実行する方法
description: WDK は、テスト バイナリと、コマンド ラインから Device Fundamental テストを簡単に実行できるようにするツールを提供します。
keywords:
- DevFund テスト
- コマンド ライン
ms.date: 06/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: de9a0d34ca201833aacb5857a3260f6f9e71bf4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340233"
---
# <a name="how-to-run-the-devfund-tests-via-the-command-line"></a>コマンド ラインから DevFund テストを実行する方法

**概要**

コマンドラインを使用して、DevFund と SysFund テストを実行するいくつかの方法はあります。  このページの手順では、Visual Studio を使用してテスト システムをプロビジョニングすることがなくが、Visual Studio と Windows Driver Kit (WDK) のコマンドラインを使用して、テストを実行します。

DevFund と SysFund テストを実行するためには、その他の方法は次のとおりです。

- ハードウェア ラボ キット (HLK):コマンドラインからテストを実行することができます、 [HLK クライアントのテスト コンピューター](https://docs.microsoft.com/windows-hardware/test/hlk/testref/reproduce-the-test-failure-by-running-the-test-from-the-command-line)

- Visual Studio を使用して「プロビジョニング」マシンをテストします。[コマンドラインから実行中のテスト](https://docs.microsoft.com/windows-hardware/drivers/develop/how-to-test-a-driver-at-runtime-from-a-command-prompt)

- Enterprise Windows Driver Kit (EWDK - は必要ありません Visual Studio)。Visual Studio がインストールされていないと、使用されませんが場合、 [EWDK を使用して、コマンドラインでテストを実行するには](https://docs.microsoft.com/windows-hardware/drivers/devtest/configure-the-machine-for-testing)

**セットアップ**


WDTF インストールでは、システムのドライバーがインストールされるため、管理者特権または管理者のコマンド プロンプトから次のコマンドを実行する必要があることに注意してください。 以下の手順では、システムのアーキテクチャは x64 を前提としています。 次の手順は、他のアーキテクチャを調整する必要があります。

**手順 1.** :[Visual Studio と Windows Driver Kit (WDK を) インストールします。](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

**手順 2** :テストを使用して、 [TAEF](https://docs.microsoft.com/windows-hardware/drivers/taef/)サービス。  

TAEF サービス (Te.service) をインストールするには```%PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\TAEF\x64```し、サービスの開始を取得するには、次のコマンドを実行します。

1. ```wex.services.exe /install:te.service``` (Te.service が正常にインストールされていることを確認する)

2. ```sc start te.service``` ("STATE"を確認しますは、' 開始\_PENDING')。

3. ```sc query te.service``` (Verify 'STATE' is 'RUNNING')

4. ```sc qc te.service``` (確認 '開始\_型' が ' 自動\_開始 ')

このディレクトリ、システムの PATH 環境変数を追加し、管理者特権でコマンド プロンプトを再起動します。

**手順 3** :インストール[WDTF](https://docs.microsoft.com/windows-hardware/drivers/wdtf/) WDTF msi ファイルの場所に移動して (```%PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\```) と目的のアーキテクチャ用のパッケージをインストールします。 場所と、インストール ログ ファイルの名前を指定 **%USERPROFILE%\Desktop\WDTFInstall.log**この例では。

 
``` 
cd %PROGRAMFILES(X86)%\Windows Kits\10\Testing\Runtimes\
```

```
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64\_en-us.msi" /l\* "%USERPROFILE%\Desktop\WDTFInstall.log"
```

WDTF MSI のインストールに WDTF **%PROGRAMFILES%\Windows Kits\10\Testing\Runtimes\WDTF** WDTF MSI がある場合でも、この例は、64 ビット WDTF MSI を使用しているため **%programfiles (x86) %**


**手順 4** :テスト マシンを構成します。

- 完全なダンプを収集、カーネル デバッガーをアタッチするようにマシンを構成します。

- テストは、コンピューターの再起動可能性があるとスリープのサイクルを制御する必要があります、ため、スリープ状態を表示、およびテスト アカウント (netplwiz.exe) への自動ログオンをオフにしないでください、マシンを構成します。 その自動ログオンを注意して使用する必要がありますに注意してください。

**手順 5** :テストを実行します。  DevFund テストは **% %PROGRAMFILES (x86) %\Windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund**します。

形式は、DevFund テストを実行するための基本的なコマンドです。

```
Te.exe Devfund_<testname>.dll /name:"<test case name>" /p:"DQ=DeviceID='<Device Instance Path of device under test from Device Manager>'" /RebootStateFile:state.xml
```

場所&lt;_テスト_ケース名_&gt;テスト、テスト バイナリの名前を指定します。

/**名前**スイッチは省略可能です。 いくつかのテスト バイナリには、複数のテストが含まれているので、/**名前**スイッチでは、テストを実行する必要がありますを指定します。 指定しない場合、バイナリのテストに含まれているすべてのテストは、シーケンスで実行されます。 バイナリのテストでテストの一覧は、次のコマンドを実行して取得できます。

```
Te.exe Devfund\<testname>.dll /list
```

Devfund など\_PnPDTest.dll には PnP 関連のテストのほとんどが含まれています。

```
Te.exe Devfund_PnPDTest_WLK_Functional.dll /list

Test Authoring and Execution Framework v10.21 for x64

    Devfund_PnPDTest_WLK_Functional.dll

        PNPDTest

            PNPDTest::PNPDisableAndEnableDevice

            PNPDTest::PNPRemoveAndRestartDevice

            PNPDTest::PNPCancelRemoveDevice

            PNPDTest::PNPCancelStopDevice

            PNPDTest::PNPTryStopAndRestartDevice

            PNPDTest::PNPTryStopDeviceRequestNewResourcesAndRestartDevice

            PNPDTest::PNPTryStopDeviceAndFailRestart

            PNPDTest::PNPSurpriseRemoveAndRestartDevice

            PNPDTest::PNPDIFRemoveAndRescanParentDevice

            PNPDTest::DisableEnhancedDeviceTestingSupport
```


このテスト バイナリから 1 つのテストを実行するコマンドは、次のようになります。

```
c:\temp\Te.exe Devfund_PnPDTest_WLK_Functional.dll /name:PNPDTest::PNPSurpriseRemoveAndRestartDevice* /p:"DQ=DeviceID='my\device\id'" /RebootStateFile:state.xml
```

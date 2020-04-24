---
ms.assetid: 52505804-4367-43F4-858D-966255CA121D
title: WDK を使った Device Fundamental テストのトラブルシューティング
description: このトピックでは、WDK を使って Device Fundamental テストを実行したときに発生する可能性のある問題の解決策について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5a9eecc731f01f5b93e966ffed3a3fa0be69c7
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364202"
---
# <a name="troubleshooting-configuration-of-driver-deployment-testing-and-debugging"></a>ドライバーの展開、テスト、およびデバッグに関する構成のトラブルシューティング

ターゲット コンピューターのプロビジョニングについては、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。 ここでは、プロビジョニング プロセスのトラブルシューティングのヒントを紹介します。

## <a name="span-idgeneral_tipsspanspan-idgeneral_tipsspanspan-idgeneral_tipsspangeneral-tips"></a><span id="General_tips"></span><span id="general_tips"></span><span id="GENERAL_TIPS"></span>一般的なヒント


-   [[Configure Computers]\(コンピューターの構成\) メニュー コマンドがアクティブでない](#configure_computers_menu_command_is_inactive)
-   [プロビジョニングが失敗する](#provisioning_fails_general_tips)

## <a name="span-idprovisioning_failsspanspan-idprovisioning_failsspanspan-idprovisioning_failsspanprovisioning-fails"></a><span id="Provisioning_fails"></span><span id="provisioning_fails"></span><span id="PROVISIONING_FAILS"></span>プロビジョニングが失敗する


-   [ネットワーク パスが見つからない](#domain_the_network_path_was_not_found)
-   [ネットワーク名が見つからない](#domain_the_network_name_cannot_be_found)
-   [リモート コンピューターにアクセスできない](#domain_could_not_access_remote_machine)

## <a name="span-iddebugger_won_t_connect_or_break_inspanspan-iddebugger_won_t_connect_or_break_inspanspan-iddebugger_won_t_connect_or_break_inspandebugger-wont-connect-or-break-in"></a><span id="Debugger_won_t_connect_or_break_in"></span><span id="debugger_won_t_connect_or_break_in"></span><span id="DEBUGGER_WON_T_CONNECT_OR_BREAK_IN"></span>デバッガーが接続またはブレーク インしない


-   [デバッガーのネットワーク接続](#debugger_wont_connect_network)
-   [デバッガーの 1394 接続](#debugger_wont_connect_1394)
-   [デバッガーのシリアル接続](#debugger_wont_connect_serial)

## <a name="span-idconfigure_computers_menu_command_is_inactivespanspan-idconfigure_computers_menu_command_is_inactivespanconfigure-computers-menu-command-is-inactive"></a><span id="configure_computers_menu_command_is_inactive"></span><span id="CONFIGURE_COMPUTERS_MENU_COMMAND_IS_INACTIVE"></span>[Configure Computers]\(コンピューターの構成\) メニュー コマンドがアクティブでない


Microsoft Visual Studio を初めて起動すると、 **[ドライバー]** メニューの **[テスト] &gt; [Configure Computers (コンピューターの構成)]** コマンドがアクティブでない (灰色表示されている) 場合があります。 約 20 秒待ってから、もう一度 **[ドライバー]** メニューをクリックすると、 **[テスト] &gt; [Configure Computers (コンピューターの構成)]** コマンドが利用できるようになります。

## <a name="span-idprovisioning_fails_general_tipsspanspan-idprovisioning_fails_general_tipsspanprovisioning-fails-general-tips"></a><span id="provisioning_fails_general_tips"></span><span id="PROVISIONING_FAILS_GENERAL_TIPS"></span>プロビジョニングが失敗する: 一般的なヒント


プロビジョニングが失敗した場合は、[コンピューターの構成] ウィンドウで一連のメッセージを確認してください。 通常、このウィンドウには、構成ログの場所も表示されます。 ログを表示し、後で参照できるようにその場所をメモしてください。

ログへのパスには、隠しフォルダーが含まれている場合があります。 たとえば、次のパスに含まれる AppData は隠しフォルダーです。

C:\\Users\\*currentUser*\\AppData\\Roaming\\Microsoft\\DriverTest\\Install

ログ ファイルの名前は次のようになります。

Driver Test Computer Configuration 20121115130459167.log

## <a name="span-iddomain_the_network_path_was_not_foundspanspan-iddomain_the_network_path_was_not_foundspanprovisioning-fails-the-network-path-was-not-found"></a><span id="domain_the_network_path_was_not_found"></span><span id="DOMAIN_THE_NETWORK_PATH_WAS_NOT_FOUND"></span>プロビジョニングが失敗する: ネットワーク パスが見つからない


ターゲット コンピューターのプロビジョニングを開始すると、"**ネットワーク パスが見つかりませんでした**" というメッセージが表示される場合があります。

ターゲット コンピューターで、 **[ネットワーク探索]** が有効になっていることと、適切なネットワーク プロファイルの **[ファイルとプリンターの共有]** が有効になっていることを確認します。 たとえば、ホスト コンピューターとターゲット コンピューターがネットワーク ドメインに参加している場合は、 **[ドメイン]** ネットワーク プロファイルのネットワーク探索、ファイルとプリンターの共有を有効にする必要があります。 詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。

ホスト コンピューターからターゲット コンピューターに ping を実行できることを確認します。 ホスト コンピューターで、コマンド プロンプト ウィンドウを開き、「**ping** *targetComputerName*」と入力します。*targetComputerName* はターゲット コンピューターの名前です。

**注**  "**ネットワーク パスが見つかりませんでした**" というメッセージが表示される前に、いくつかのメッセージが表示される場合があります。 これらのメッセージの一部を読むと、ネットワーク パスが見つかり、プロビジョニングの最初の手順が成功したと思うかもしれませんが、 実際には、ネットワーク パスは見つからず、プロビジョニングは成功していません。 たとえば、次のようなメッセージが表示される場合があります。

 

```cpp
Connecting to computer "MyComputer"
Installing driver test automation service
Getting computer system information
Copying driver test automation files
The network path was not found.
```

## <a name="span-iddomain_the_network_name_cannot_be_foundspanspan-iddomain_the_network_name_cannot_be_foundspanprovisioning-fails-the-network-name-cannot-be-found"></a><span id="domain_the_network_name_cannot_be_found"></span><span id="DOMAIN_THE_NETWORK_NAME_CANNOT_BE_FOUND"></span>プロビジョニングが失敗する: ネットワーク名が見つからない


ターゲット コンピューターのプロビジョニングを開始すると、 **"ネットワーク名が見つかりません"** というメッセージが表示される場合があります。 ターゲット コンピューターの名前をもう一度確認します。 最初に入力したコンピューター名が正しくなかった場合は、( **[ドライバー] &gt; [テスト] &gt; [Configure Computers (コンピューターの構成)]** の順にクリックして) もう一度プロビジョニング ウィザードを開始します。 間違ったコンピューター名を選び、 **[次へ]** をクリックします。 **[コンピューター名]** に、ターゲット コンピューターの正しい名前を入力し、ウィザードを完了します。

**注**  "**ネットワーク名が見つかりませんでした**" というメッセージが表示される前に、いくつかのメッセージが表示される場合があります。 これらのメッセージの一部を読むと、コンピューター名が見つかり、プロビジョニングの最初の手順が成功したと思うかもしれませんが、 実際には、コンピューター名は見つからず、プロビジョニングは成功していません。 たとえば、次のようなメッセージが表示される場合があります。

 

```cpp
Connecting to computer "NonExistentComputer"
Installing driver test automation service
Getting computer system information
Copying driver test automation files
The network name cannot be found.
```

**注**  間違ったターゲット コンピューター名を入力したときに表示されるメッセージはさまざまです。 たとえば、ネットワーク探索の有効化についてのメッセージが表示される場合があります。

 

```cpp
Connecting to computer "NonExistentComputer"
Installing driver test automation service
Could not access remote machine "NonExistentComputer" over the network. 
Error:53. Automatic configuration of machines over the network requires
that network discovery and file and print sharing be enabled on the 
target machine.
```

また、資格情報の入力を求めるメッセージが表示される場合もあります。

```cpp
Enter your password to connect to: NonExistentComputer
```

## <a name="span-iddomain_could_not_access_remote_machinespanspan-iddomain_could_not_access_remote_machinespanprovisioning-fails-could-not-access-remote-machine"></a><span id="domain_could_not_access_remote_machine"></span><span id="DOMAIN_COULD_NOT_ACCESS_REMOTE_MACHINE"></span>プロビジョニングが失敗する: リモート コンピューターにアクセスできない


ターゲット コンピューターのプロビジョニングを開始すると、"**Could not access the remote machine** "*computerName*" **over the network**" (ネットワーク経由でリモート コンピューター "computerName" にアクセスできませんでした) というメッセージが表示される場合があります。 このメッセージが表示される理由はいくつかあります。 ホスト コンピューターとターゲット コンピューターの両方が同じドメインまたは同じワークグループに参加していることを確認します。 詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。 ターゲット コンピューターの正しい名前を入力したことを確認します。 ターゲット コンピューターで、ネットワーク探索、ファイルとプリンターの共有を有効にしていることを確認します。

## <a name="debugger-breakpoints-are-not-triggered-for-kernel-mode-driver"></a>カーネル モード ドライバーの場合にデバッガーのブレークポイントがトリガーされない


1. ブレークポイントを無効にしてドライバーを展開します。 
2. 手動でカーネル モード デバッガーに割り込みます。 
3. モジュールの読み込み時に例外を設定します。
   ```cpp
   sxe ld <DriverName>
   ``` 
4. ブレークポイントを有効にして、実行を再開します。 
5. ターゲット コンピューターで、デバイス ノードを無効にしてから再び有効にします。 

## <a name="span-iddebugger_wont_connect_networkspanspan-iddebugger_wont_connect_networkspandebugger-wont-connect-or-break-in-network-connection"></a><span id="debugger_wont_connect_network"></span><span id="DEBUGGER_WONT_CONNECT_NETWORK"></span>デバッガーが接続またはブレーク インしない: ネットワーク接続


デバッグ アプリケーションがどの種類のネットワークのファイアウォールでも許可されていることを確認します。

ネットワーク デバッグを許可するポートについて、ネットワーク管理者に問い合わせます。

ターゲット コンピューターに複数のネットワーク アダプターがある場合は、デバッグに使うネットワーク アダプターのバス パラメーターを指定する必要があります。

詳しくは、「[ネットワーク ケーブル経由のデバッグのトラブルシューティングのヒント](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)」をご覧ください。

## <a name="span-iddebugger_wont_connect_1394spanspan-iddebugger_wont_connect_1394spandebugger-wont-connect-or-break-in-1394-connection"></a><span id="debugger_wont_connect_1394"></span><span id="DEBUGGER_WONT_CONNECT_1394"></span>デバッガーが接続またはブレーク インしない: 1394 接続


ターゲット コンピューターに複数の 1394 コントローラーがある場合は、デバッグに使う 1394 コントローラーのバス パラメーターを指定する必要があります。 詳しくは、「[1394 ケーブル経由のデバッグのトラブルシューティングのヒント](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-1394-cable-connection)」をご覧ください。

## <a name="span-iddebugger_wont_connect_serialspanspan-iddebugger_wont_connect_serialspandebugger-wont-connect-or-break-in--serial-connection"></a><span id="debugger_wont_connect_serial"></span><span id="DEBUGGER_WONT_CONNECT_SERIAL"></span>デバッガーが接続またはブレーク インしない: シリアル接続


ホスト コンピューターとターゲット コンピューターの COM ポート番号を確認します。 ホスト コンピューターとターゲット コンピューターの両方でデバッグに同じボー レートを構成したことを確認します。 詳しくは、「[シリアル ケーブル経由のデバッグのトラブルシューティングのヒント](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-null-modem-cable-connection-in-visual-studio)」をご覧ください。

 

 






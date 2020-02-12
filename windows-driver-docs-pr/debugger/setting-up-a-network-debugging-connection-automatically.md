---
title: KDNET ネットワーク カーネル デバッグの自動設定
description: KDNET を使用して、Windows デバッグツール用にネットワークカーネルデバッグを自動的に構成します。
ms.assetid: B4A79B2E-D4B1-42CA-9121-DEC923C76927
keywords:
- ネットワークデバッグ
- イーサネットデバッグ
- WinDbg
- KDNET
ms.date: 09/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 76f5bb9dd746a6dbd2d926cff72a1bc816fc2cc0
ms.sourcegitcommit: 331d113b4d78d64ba82fa4c9f0b895afabb5cb3b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77144698"
---
# <a name="setting-up-kdnet-network-kernel-debugging-automatically"></a>KDNET ネットワーク カーネル デバッグの自動設定

Windows 用デバッグツールでは、ネットワーク経由のカーネルデバッグがサポートされています。 このトピックでは、kdnet セットアップツールを使用してネットワークデバッグを自動的に設定する方法について説明します。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。 ホストコンピューターは、Windows 7 以降を実行している必要があります。また、対象のコンピューターで Windows 8 以降が実行されている必要があります。

## <a name="span-iddetermining_the_ip_address_of_the_host_computerspanspan-iddetermining_the_ip_address_of_the_host_computerspanspan-iddetermining_the_ip_address_of_the_host_computerspandetermining-the-ip-address-of-the-host-computer"></a><span id="Determining_the_IP_Address_of_the_Host_Computer"></span><span id="determining_the_ip_address_of_the_host_computer"></span><span id="DETERMINING_THE_IP_ADDRESS_OF_THE_HOST_COMPUTER"></span>ホストコンピューターの IP アドレスを確認する

1. ターゲットおよびホスト Pc がネットワークハブに接続されていること、または適切なネットワークケーブルを使用してスイッチが接続されていることを確認します。 

2. ホストコンピューターで、コマンドプロンプトウィンドウを開き、「 *IPConfig* 」と入力して IP 構成を表示します。 

3. コマンドの出力で、イーサネットアダプターの IPv4 アドレスを見つけます。

    ```console
    ...

    Ethernet adapter Ethernet:
    ...

    IPv4 Address. . . . . . . . . . . : <YourHostIPAddress>
    ...

    ```
4. デバッグに使用するネットワークアダプターの IPv4 アドレスをメモしておきます。

 

## <a name="span-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspanspan-idsetting_up_the_target_computerspansetting-up-the-host-and-target-computers"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>ホストとターゲットコンピューターの設定

次の手順に従って、kdnet ユーティリティを使用して、ターゲット PC でデバッガーの設定を自動的に構成します。

1. Windows デバッグツールがホストシステムにインストールされていることを確認します。 デバッガーツールのダウンロードとインストールの詳細については、「 [Windows 用デバッグツールのダウンロード](debugger-download-tools.md)」を参照してください。 

2. *Kdnet*ファイルと*VerifiedNICList*ファイルを見つけます。 既定では、これらはここにあります。

   ```console
   C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
   ```

   > [!NOTE]
   > これらの方法では、両方の Pc がターゲットとホストの両方で64ビットバージョンの Windows を実行していることを前提としています。 そうでない場合は、ターゲットが実行されているホストで同じ "ビット" のツールを実行するのが最善の方法です。 たとえば、ターゲットが32ビットの Windows を実行している場合は、ホストで32バージョンのデバッガーを実行します。 詳細については、「 [32 ビットまたは64ビットのデバッグツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)」を参照してください。
   > 

3. ホストコンピューターで、2つのファイルをネットワーク共有またはサムドライブにコピーして、対象のコンピューターで使用できるようにします。

4. ターゲットコンピューターで、C:\KDNET ディレクトリを作成し、 *KDNET*ファイルと*VerifiedNICList*ファイルをそのディレクトリにコピーします。

   > [!IMPORTANT]
   > Kdnet を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows セキュリティ機能を一時的に停止することが必要になる場合があります。
   > セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。


5. ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力して、ターゲットコンピューターにサポートされているネットワークアダプターがあることを確認します。

   ```console
   C:\KDNET>kdnet.exe
   Network debugging is supported on the following NICs:
   busparams=1.0.0, Broadcom NetXtreme Gigabit Ethernet, Plugged in.  
   This Microsoft hypervisor supports using KDNET in guest VMs.
   ```

6. Kdnet からの出力は、ターゲットのネットワークアダプターがサポートされていることを示しているので、続行できます。

7. 次のコマンドを入力して、ホストシステムの IP アドレスを設定し、一意の接続キーを生成します。 IP アドレスまたはホストシステムの名前を使用します。 推奨される50000-50039 の範囲内で、使用するターゲット/ホストペアごとに一意のポートアドレスを選択します。

   ```console
   C:\>kdnet.exe <HostComputerIPAddress> <YourDebugPort> 
   
   Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
   Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
   ```

8. 返されたキーを notepad.exe ファイルにコピーします。


## <a name="span-idusing_windbgspanspan-idusing_windbgspanspan-idusing_windbgspan-using-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span>WinDbg の使用

ホストコンピューターで、[WinDbg] を開きます。 **[ファイル]** メニューの **[カーネルデバッグ]** をクリックします。 カーネルデバッグ ダイアログボックスで、 **Net** タブを開きます。前の手順でメモ帳の .txt ファイルに保存したポート番号とキーを貼り付けます。 **[OK]** をクリックすると、

また、コマンドプロンプトウィンドウを開き、次のコマンドを入力して、WinDbg セッションを開始することもできます。 <YourPort> は上で選択したポートで、<YourKey> は上の kdnet によって返されたキーです。 前の手順でメモ帳の .txt ファイルに保存したのキーを貼り付けます。

   ```console
  windbg -k net:port=<YourDebugPort>,key=<YourKey> 
   ```

ファイアウォール経由でのポートへのアクセスを WinDbg に許可するように求めるメッセージが表示された場合は、他の**3 つ**の種類のネットワークすべてに対して、windbg がポートにアクセスできるようにします。

![windows セキュリティの警告-windows ファイアウォールがこのアプリの一部の機能をブロックしました ](images/debuglab-image-firewall-dialog-box.png)

この時点で、デバッガーはターゲットが再接続するのを待機し、次のようなテキストがデバッガーのコマンドウィンドウに表示されます。

   ```console
   Microsoft (R) Windows Debugger Version 1.0.1908.30002 AMD64
   Copyright (c) Microsoft Corporation. All rights reserved.

   Using NET for debugging
   Opened WinSock 2.0
   Waiting to reconnect...
   ```

## <a name="span-idrestarting_targetspanspan-idrestarting_targetspanspan-idrestarting_targetspan-restarting-the-target-pc"></a><span id="Restarting_Target"></span><span id="restarting_target"></span><span id="RESTARTING_TARGET"></span>ターゲット PC を再起動する

デバッガーが "再接続を待機しています..." になったら、ステージングし、ターゲットコンピューターを再起動します。 PC を再起動する1つの方法は、管理者のコマンドプロンプトからこのコマンドを使用することです。

   ```console
   shutdown -r -t 0 
   ```

対象の PC が再起動すると、デバッガーは自動的に接続されます。

## <a name="span-idtroubleshooting_tipsspanspan-idtroubleshooting_tipsspantroubleshooting-tips"></a><span id="troubleshooting_tips"></span><span id="TROUBLESHOOTING_TIPS"></span>トラブルシューティングのヒント

**デバッグアプリケーションはファイアウォール経由で許可されている必要があります**

デバッガーは、ファイアウォール経由のアクセス権を持っている必要があります。 コントロールパネルを使用して、ファイアウォール経由のアクセスを許可します。 

1. **コントロールパネルを開き &gt; システムとセキュリティ** をクリックし、**Windows ファイアウォールを介したアプリの許可** をクリックします。 

2. アプリケーションの一覧で、 *WINDOWS GUI のシンボリックデバッガー*と*windows カーネルデバッガー*を見つけます。 

3. チェックボックスを使用して、これら2つのアプリケーションがファイアウォールを介して、3種類のネットワークの種類を**すべて**許可するようにします。 

4. 下にスクロールし、 **[OK]** をクリックして、ファイアウォールの変更を保存します。 デバッガーを再起動します。

    ![3種類のネットワークをすべて有効にした windows GUI シンボリックデバッガーと Windows カーネルデバッガーを表示する windows コントロールパネルのファイアウォール構成](images/firewall-control-pannel-windbg-gui-config.png)

**Ping を使用して接続をテストする**

デバッガーがタイムアウトになり、接続できない場合は、ターゲット PC で ping コマンドを使用して接続を確認します。 

   ```console
   C:\>Ping <HostComputerIPAddress> 
   ```

**ネットワークデバッグ用のポートの選択**

デバッガーがタイムアウトになり、接続できない場合は、既定のポート番号5万が既に使用されているか、ブロックされている可能性があります。 

49152 ~ 65535 の任意のポート番号を選択できます。 推奨される範囲は 5万 ~ 50039 です。 選択したポートは、ホストコンピューターで実行されているデバッガーによる排他アクセスのために開かれます。 

ネットワークデバッグに使用できるポート番号の範囲は、会社のネットワークポリシーによって制限さ**れる  ます**。 会社のポリシーによってネットワークデバッグに使用できるポートの範囲が制限されているかどうかを確認するには、ネットワーク管理者に確認してください。

**サポートされているネットワークアダプター**

Kdnet の実行時に "ネットワークデバッグがこのコンピューターのどの Nic でもサポートされていません" と表示される場合は、ネットワークアダプターがサポートされていないことを意味します。 

ホストコンピューターは任意のネットワークアダプターを使用できますが、ターゲットコンピューターでは、Windows 用デバッグツールでサポートされているネットワークアダプターを使用する必要があります。 サポートされているネットワークアダプターの一覧については、「 [Windows 10 でサポートされるイーサネット nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md) 」および「 [Windows 8.1 でネットワークカーネルデバッグ用にサポートされるイーサネット nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Windows 10 でのネットワークカーネルデバッグ用にサポートされているイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

[Windows 8.1 でのネットワークカーネルデバッグ用にサポートされるイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[KDNET Network カーネルデバッグの手動設定](setting-up-a-network-debugging-connection.md)

[WinDbg ドライバーの概要 (カーネル モード)](getting-started-with-windbg--kernel-mode-.md)

[ユニバーサル ドライバーのデバッグ - ステップ バイ ステップ ラボ (Echo カーネル モード)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)
